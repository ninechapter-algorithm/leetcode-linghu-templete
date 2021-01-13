# 停车场
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/parking-lot/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一个停车场
1. 一共有*n*层，每层*m*列，每列*k*个位置
2. 停车场可以停摩托车，公交车，汽车
3. 停车位分别有摩托车位，汽车位，大型停车位
4. 每一列，摩托车位编号范围为`[0,k/4)(注：包括0，不包括k/4)`,汽车停车位编号范围为`[k/4,k/4*3)(注：不包括k/4*3)`,大型停车位编号范围为`[k/4*3,k)(注：不包括k)`
5. 一辆摩托车可以停在任何停车位
6. 一辆汽车可以停在一个汽车位或者大型停车位
7. 一辆公交车可以停在一列里的连续5个大型停车位。
 ### 样例说明
 
 ### 参考代码
 ```java
// enum type for Vehicle
enum VehicleSize {
	Motorcycle,
	Compact,
	Large,
}

//abstract Vehicle class
abstract class Vehicle {
    // Write your code here
	protected int spotsNeeded;
	protected VehicleSize size;
	protected String licensePlate;  // id for a vehicle

	protected ArrayList<ParkingSpot> parkingSpots = new ArrayList<ParkingSpot>(); // id for parking where may occupy multi

	public int getSpotsNeeded() {
		return spotsNeeded;
	}
	
	public VehicleSize getSize() {
		return size;
	}

	/* Park vehicle in this spot (among others, potentially) */
	public void parkInSpot(ParkingSpot spot) {
		parkingSpots.add(spot);
	}
	
	/* Remove car from spot, and notify spot that it's gone */
	public void clearSpots() {
		for (int i = 0; i < parkingSpots.size(); i++) {
			parkingSpots.get(i).removeVehicle();
		}
		parkingSpots.clear();
	}
	//this need to be implement in subclass
	public abstract boolean canFitInSpot(ParkingSpot spot);
    public abstract void print(); 
}

class Motorcycle extends Vehicle {
    // Write your code here
	public Motorcycle() {
		spotsNeeded = 1;
		size = VehicleSize.Motorcycle;
	}
	
	public boolean canFitInSpot(ParkingSpot spot) {
		return true;
	}
    
    public void print() {  
        System.out.print("M");  
    }
}

class Car extends Vehicle {
    // Write your code here
	public Car() {
		spotsNeeded = 1;
		size = VehicleSize.Compact;
	}
	
	public boolean canFitInSpot(ParkingSpot spot) {
		return spot.getSize() == VehicleSize.Large || spot.getSize() == VehicleSize.Compact;
	}

    public void print() {  
        System.out.print("C");  
    } 
}

class Bus extends Vehicle {
    // Write your code here
	public Bus() {
		spotsNeeded = 5;
		size = VehicleSize.Large;
	}

	public boolean canFitInSpot(ParkingSpot spot) {
		return spot.getSize() == VehicleSize.Large;
	}

    public void print() {  
        System.out.print("B");  
    } 
}

class ParkingSpot {
    // Write your code here
	private Vehicle vehicle;
	private VehicleSize spotSize;
	private int row;
	private int spotNumber;
	private Level level;

	public ParkingSpot(Level lvl, int r, int n, VehicleSize sz) {
		level = lvl;
		row = r;
		spotNumber = n;
		spotSize = sz;
	}
	
	public boolean isAvailable() {
		return vehicle == null;
	}
	/* Checks if the spot is big enough for the vehicle (and is available). This compares
	 * the SIZE only. It does not check if it has enough spots. */
	public boolean canFitVehicle(Vehicle vehicle) {
		return isAvailable() && vehicle.canFitInSpot(this);
	}
	/* Park vehicle in this spot. */
	public boolean park(Vehicle v) {
		if (!canFitVehicle(v)) {
			return false;
		}
		vehicle = v;
		vehicle.parkInSpot(this);
		return true;
	}
	/* Remove vehicle from spot, and notify level that a new spot is available */
	public void removeVehicle() {
		level.spotFreed();
		vehicle = null;
	}
	
	public int getRow() {
		return row;
	}
	
	public int getSpotNumber() {
		return spotNumber;
	}
	
	public VehicleSize getSize() {
		return spotSize;
	}

    public void print() {  
        if (vehicle == null) {  
            if (spotSize == VehicleSize.Compact) {  
                System.out.print("c");  
            } else if (spotSize == VehicleSize.Large) {  
                System.out.print("l");  
            } else if (spotSize == VehicleSize.Motorcycle) {  
                System.out.print("m");  
            }  
        } else {  
            vehicle.print();  
        }  
    }
}

/* Represents a level in a parking garage */
class Level {
    // Write your code here
	private int floor;
	private ParkingSpot[] spots;
	private int availableSpots = 0; // number of free spots
	private int SPOTS_PER_ROW;


	public Level(int flr, int num_rows, int spots_per_row) {
		floor = flr;
        int SPOTS_PER_ROW = spots_per_row;
        int numberSpots  = 0;
		spots = new ParkingSpot[num_rows * spots_per_row];

		//init size for each spot in array spots
        for (int row = 0; row < num_rows; ++row) {
            for (int spot = 0; spot < spots_per_row / 4; ++spot) {
                VehicleSize sz = VehicleSize.Motorcycle;
                spots[numberSpots] = new ParkingSpot(this, row, numberSpots, sz);
                numberSpots ++;
            }
            for (int spot = spots_per_row / 4; spot < spots_per_row / 4 * 3; ++spot) {
                VehicleSize sz = VehicleSize.Compact;
                spots[numberSpots] = new ParkingSpot(this, row, numberSpots, sz);
                numberSpots ++;
            }
            for (int spot = spots_per_row / 4 * 3; spot < spots_per_row; ++spot) {
                VehicleSize sz = VehicleSize.Large;
                spots[numberSpots] = new ParkingSpot(this, row, numberSpots, sz);
                numberSpots ++;
            }
        }

        availableSpots = numberSpots;
	}

	/* Try to find a place to park this vehicle. Return false if failed. */
	public boolean parkVehicle(Vehicle vehicle) {
		if (availableSpots() < vehicle.getSpotsNeeded()) {
			return false; // no enough spots
		}
		int spotNumber = findAvailableSpots(vehicle);
		if(spotNumber < 0) {
			return false;
		}
		return parkStartingAtSpot(spotNumber, vehicle);
	}

	/* find a spot to park this vehicle. Return index of spot, or -1 on failure. */
	private int findAvailableSpots(Vehicle vehicle) {
		int spotsNeeded = vehicle.getSpotsNeeded();
		int lastRow = -1;
		int spotsFound = 0;

		for(int i = 0; i < spots.length; i++){
			ParkingSpot spot = spots[i];
			if(lastRow != spot.getRow()){
				spotsFound = 0;
				lastRow = spot.getRow();
			}
			if(spot.canFitVehicle(vehicle)){
				spotsFound++;
			}else{
				spotsFound = 0;
			}
			if(spotsFound == spotsNeeded){
				return i - (spotsNeeded - 1); // index of spot
			}
		}
		return -1;
	}

	/* Park a vehicle starting at the spot spotNumber, and continuing until vehicle.spotsNeeded. */
	private boolean parkStartingAtSpot(int spotNumber, Vehicle vehicle) {
		vehicle.clearSpots();

		boolean success = true;
		
		for (int i = spotNumber; i < spotNumber + vehicle.spotsNeeded; i++) {
			 success &= spots[i].park(vehicle);
		}
		
		availableSpots -= vehicle.spotsNeeded;
		return success;
	}

	/* When a car was removed from the spot, increment availableSpots */
	public void spotFreed() {
		availableSpots++;
	}

	public int availableSpots() {
		return availableSpots;
	}

    public void print() {  
        int lastRow = -1;  
        for (int i = 0; i < spots.length; i++) {  
            ParkingSpot spot = spots[i];  
            if (spot.getRow() != lastRow) {  
                System.out.print("  ");  
                lastRow = spot.getRow();  
            }  
            spot.print();  
        }  
    }
}

public class ParkingLot {
	private Level[] levels;
	private int NUM_LEVELS;
	
    // @param n number of leves
    // @param num_rows  each level has num_rows rows of spots
    // @param spots_per_row each row has spots_per_row spots
	public ParkingLot(int n, int num_rows, int spots_per_row) {
        // Write your code here
        NUM_LEVELS = n;
		levels = new Level[NUM_LEVELS];
		for (int i = 0; i < NUM_LEVELS; i++) {
			levels[i] = new Level(i, num_rows, spots_per_row);
		}
	}

	// Park the vehicle in a spot (or multiple spots)
    // Return false if failed
	public boolean parkVehicle(Vehicle vehicle) {
        // Write your code here
		for (int i = 0; i < levels.length; i++) {
			if (levels[i].parkVehicle(vehicle)) {
				return true;
			}
		}
		return false;
	}

    // unPark the vehicle
	public void unParkVehicle(Vehicle vehicle) {
        // Write your code here
		vehicle.clearSpots();
	}

    public void print() {  
        for (int i = 0; i < levels.length; i++) {  
            System.out.print("Level" + i + ": ");  
            levels[i].print();
            System.out.println("");  
        }  
        System.out.println("");  
    } 
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)