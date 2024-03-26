import java.util.*;

class Plane {
    private int ID;
    private String name;
    private int year;

    public Plane(int ID, String name, int year) {
        this.ID = ID;
        this.name = name;
        this.year = year;
    }

    public int getID() {
        return ID;
    }

    public String getName() {
        return name;
    }

    public int getYear() {
        return year;
    }

    @Override
    public String toString() {
        return "Plane{" +
                "ID=" + ID +
                ", name='" + name + '\'' +
                ", year=" + year +
                '}';
    }
}

public class Main {
    public static void main(String[] args) {
        Set<Plane> planes = new HashSet<>();
        Random random = new Random();

        for (int i = 1; i <= 100; i++) {
            planes.add(new Plane(i, "Plane" + i, 2000 + random.nextInt(20)));
        }

        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("Menu:");
            System.out.println("1) Sort by name");
            System.out.println("2) Sort by year");
            System.out.println("3) Filter by name");
            System.out.println("4) Filter by year");
            System.out.println("5) Filter by specified year");
            System.out.println("0) Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    planes.stream()
                            .sorted(Comparator.comparing(Plane::getName))
                            .forEach(System.out::println);
                    break;
                case 2:
                    planes.stream()
                            .sorted(Comparator.comparing(Plane::getYear))
                            .forEach(System.out::println);
                    break;
                case 3:
                    System.out.print("Enter a letter to filter by name: ");
                    String letter = scanner.next();
                    planes.stream()
                            .filter(plane -> plane.getName().contains(letter))
                            .forEach(System.out::println);
                    break;
                case 4:
                    System.out.print("Enter a year to filter by: ");
                    int filterYear = scanner.nextInt();
                    planes.stream()
                            .filter(plane -> plane.getYear() == filterYear)
                            .forEach(System.out::println);
                    break;
                case 5:
                    System.out.print("Enter a year to get the count of planes: ");
                    int specifiedYear = scanner.nextInt();
                    long count = planes.stream()
                            .filter(plane -> plane.getYear() == specifiedYear)
                            .count();
                    System.out.println("Number of planes produced in " + specifiedYear + ": " + count);
                    break;
            }
        } while (choice != 0);
    }
}
