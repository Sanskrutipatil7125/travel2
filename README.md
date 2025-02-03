import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Destination {
    int id;
    String name;
    String country;
    String description;

    public Destination(int id, String name, String country, String description) {
        this.id = id;
        this.name = name;
        this.country = country;
        this.description = description;
    }

    @Override
    public String toString() {
        return id + ". " + name + " - " + country + " (" + description + ")";
    }
}

class Booking {
    String userName;
    int destinationId;

    public Booking(String userName, int destinationId) {
        this.userName = userName;
        this.destinationId = destinationId;
    }

    @Override
    public String toString() {
        return "Booking: " + userName + " -> Destination ID " + destinationId;
    }
}

public class TravelApp {
    private static final Scanner scanner = new Scanner(System.in);
    private static final List<Destination> destinations = new ArrayList<>();
    private static final List<Booking> bookings = new ArrayList<>();
    private static int destinationCounter = 1;

    public static void main(String[] args) {
        // Preload some destinations
        destinations.add(new Destination(destinationCounter++, "Eiffel Tower", "France", "A famous landmark in Paris"));
        destinations.add(new Destination(destinationCounter++, "Great Wall of China", "China", "An ancient wall spanning thousands of miles"));

        while (true) {
            System.out.println("\nTravel App");
            System.out.println("1. View Destinations");
            System.out.println("2. Add Destination");
            System.out.println("3. Book a Trip");
            System.out.println("4. View Bookings");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    viewDestinations();
                    break;
                case 2:
                    addDestination();
                    break;
                case 3:
                    bookTrip();
                    break;
                case 4:
                    viewBookings();
                    break;
                case 5:
                    System.out.println("Exiting... Safe Travels!");
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Try again.");
            }
        }
    }

    private static void viewDestinations() {
        if (destinations.isEmpty()) {
            System.out.println("No destinations available.");
            return;
        }

        System.out.println("\nAvailable Destinations:");
        for (Destination d : destinations) {
            System.out.println(d);
        }
    }

    private static void addDestination() {
        System.out.print("Enter Destination Name: ");
        String name = scanner.nextLine();
        System.out.print("Enter Country: ");
        String country = scanner.nextLine();
        System.out.print("Enter Description: ");
        String description = scanner.nextLine();

        destinations.add(new Destination(destinationCounter++, name, country, description));
        System.out.println("Destination added successfully!");
    }

    private static void bookTrip() {
        if (destinations.isEmpty()) {
            System.out.println("No destinations available to book.");
            return;
        }

        System.out.print("Enter your name: ");
        String userName = scanner.nextLine();
        System.out.print("Enter Destination ID: ");
        int destinationId = scanner.nextInt();
        scanner.nextLine(); // Consume newline

        boolean destinationExists = false;
        for (Destination d : destinations) {
            if (d.id == destinationId) {
                destinationExists = true;
                break;
            }
        }

        if (destinationExists) {
            bookings.add(new Booking(userName, destinationId));
            System.out.println("Trip booked successfully!");
        } else {
            System.out.println("Invalid Destination ID. Try again.");
        }
    }

    private static void viewBookings() {
        if (bookings.isEmpty()) {
            System.out.println("No bookings available.");
            return;
        }

        System.out.println("\nYour Bookings:");
        for (Booking b : bookings) {
            System.out.println(b);
        }
    }
}
