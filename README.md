# OOP-3-Lab
import java.util.Scanner;

// Vehicle: Base class for various vehicle types
abstract class Vehicle {
    private String color;
    private int speed;

    public Vehicle(String color, int speed) {
        this.color = color;
        this.speed = speed;
    }

    // move: Display moving vehicle with its speed
    public void move() {
        System.out.println("The " + color + " vehicle is moving at " + speed + " mph.");
    }

    // startEngine: Display message indicating the engine has started
    public void startEngine() {
        System.out.println("The engine is started");
    }
}

// Car: Abstract class with common properties/methods for car subclasses
abstract class Car extends Vehicle {
    private int price; // in USD

    public Car(String color, int speed, int price) {
        super(color, speed);
        this.price = price;
    }

    public int getPrice() {
        return price;
    }

    // calculateDepreciation: Recursively calculate the car's depreciated value over years
    public int calculateDepreciation(int currentPrice, double depreciationRate, int years) {
        if (years == 0) {
            return currentPrice;
        } else {
            int depreciatedPrice = (int) (currentPrice * (1 - depreciationRate));
            System.out.println("Year " + (years) + " value: $" + depreciatedPrice);
            return calculateDepreciation(depreciatedPrice, depreciationRate, years - 1);
        }
    }

    // calculateDistance: Recursively calculate distance traveled
    public int calculateDistance(int speed, int time) {
        if (time == 0) {
            return 0;
        } else {
            return speed + calculateDistance(speed, time - 1);
        }
    }

    // calculateTotalServiceCost: Recursively calculate total service cost over years
    public int calculateTotalServiceCost(int annualServiceCost, int years) {
        if (years == 0) {
            return 0;
        } else {
            System.out.println("Year " + (years) + " service cost: $" + annualServiceCost);
            return annualServiceCost + calculateTotalServiceCost(annualServiceCost, years - 1);
        }
    }

    // findMaximumSpeed: Recursively find the maximum speed from an array of speeds
    public int findMaximumSpeed(int[] speeds, int index) {
        if (index == 1) {
            return speeds[0];
        } else {
            return Math.max(speeds[index - 1], findMaximumSpeed(speeds, index - 1));
        }
    }

    // calculateInsurancePrice: Recursively calculate total insurance cost over years
    public int calculateInsurancePrice(int price, double riskFactor, int years) {
        if (years <= 0) {
            return 0;
        } else {
            int thisYearInsurance = (int) (price * riskFactor);
            System.out.println("Year " + (years) + " insurance cost: $" + thisYearInsurance);
            return thisYearInsurance + calculateInsurancePrice(price, riskFactor * 0.95, years - 1);
        }
    }
}

// Following classes (ElectricCar, SportsCar, SUV, Convertible) extend Car and add unique properties/methods

class ElectricCar extends Car {
    private int batteryCapacity;

    public ElectricCar(String color, int speed, int batteryCapacity, int price) {
        super(color, speed, price);
        this.batteryCapacity = batteryCapacity;
    }

    public void charge() {
        System.out.println("The electric car is charging.");
    }
}

class SportsCar extends Car {
    private int maxSpeed;

    public SportsCar(String color, int speed, int maxSpeed, int price) {
        super(color, speed, price);
        this.maxSpeed = maxSpeed;
    }

    public void boost() {
        System.out.println("The sports car is boosting its speed to " + maxSpeed + " mph.");
    }
}

class SUV extends Car {
    private int cargoSpace;

    public SUV(String color, int speed, int cargoSpace, int price) {
        super(color, speed, price);
        this.cargoSpace = cargoSpace;
    }

    public void offRoad() {
        System.out.println("The SUV is going off-road.");
    }
}

class Convertible extends Car {
    private boolean isTopDown;

    public Convertible(String color, int speed, boolean isTopDown, int price) {
        super(color, speed, price);
        this.isTopDown = isTopDown;
    }

    public void toggleRoof() {
        if (isTopDown) {
            isTopDown = false;
            System.out.println("The convertible's roof is now up.");
        } else {
            isTopDown = true;
            System.out.println("The convertible's roof is now down.");
        }
    }
}

class MainClass {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Car chosenCar = null;

        // Continuously prompt the user until they choose to exit
        while (true) {
            System.out.println("Choose a vehicle type: ");
            System.out.println("1. Electric Car");
            System.out.println("2. Sports Car");
            System.out.println("3. SUV");
            System.out.println("4. Convertible");
            System.out.println("5. Exit");
            System.out.print("Enter the number corresponding to your choice: ");

            int choice = scanner.nextInt();

            // Exit the loop (and thus the program) if the user chooses to exit
            if (choice == 5) {
                System.out.println("Goodbye!");
                break;
            }

            // Vehicle selection
            switch (choice) {
                case 1:
                    chosenCar = new ElectricCar("White", 120, 100, 79999);
                    break;
                case 2:
                    chosenCar = new SportsCar("Red", 150, 200, 99999);
                    break;
                case 3:
                    chosenCar = new SUV("Black", 100, 50, 49999);
                    break;
                case 4:
                    chosenCar = new Convertible("Yellow", 110, true, 69999);
                    break;
                default:
                    System.out.println("Invalid choice!");
                    continue; // Invalid choice, retry the loop
            }

            // [Assuming chosenCar is not null] Display the information and call the recursive methods:
            chosenCar.move();
            chosenCar.startEngine();
            System.out.println("Price: $" + chosenCar.getPrice());

            // Call the method that recursively calculates and displays depreciation over 5 years and prints the depreciated price
            int depreciatedPrice = chosenCar.calculateDepreciation(chosenCar.getPrice(), 0.15, 5);
            System.out.println("Depreciated price after 5 years: $" + depreciatedPrice);

            // Call the method that recursively calculates the distance traveled given speed and time
            int distance = chosenCar.calculateDistance(60, 5);  
            System.out.println("Distance traveled in 5 hours at 60 mph: " + distance + " miles");

            // Call the method that recursively calculates and displays the total service cost over 5 years
            int totalServiceCost = chosenCar.calculateTotalServiceCost(500, 5);  
            System.out.println("Total service cost over 5 years: $" + totalServiceCost);

            // Call the method that recursively finds the maximum speed from an array of speeds
            int[] speeds = {120, 150, 110, 130, 125};
            int maxSpeed = chosenCar.findMaximumSpeed(speeds, speeds.length);
            System.out.println("Maximum recorded speed: " + maxSpeed + " mph");

            // Call the method that recursively calculates and displays the insurance cost over 5 years, reducing risk each year
            int totalInsuranceCost = chosenCar.calculateInsurancePrice(chosenCar.getPrice(), 0.05, 5);
            System.out.println("Total insurance cost over 5 years: $" + totalInsuranceCost);

            System.out.println("\n");
        }

        scanner.close(); // Close the Scanner when finished
    }
}
