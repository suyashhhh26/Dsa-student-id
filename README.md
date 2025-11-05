package Demo;
import java.util.Scanner;

public class StudentSearch {

    public static int linearSearch(int[] ids, int targetId) {
        for (int i = 0; i < ids.length; i++) {
            if (ids[i] == targetId) return i;
    }
        return -1;
    }

    public static void sortById(int[] ids, String[] names, String[] departments) {
        int n = ids.length;
        boolean swapped;
        for (int i = 0; i < n - 1; i++) {
            swapped = false;
            for (int j = 0; j < n - i - 1; j++) {
                if (ids[j] > ids[j + 1]) {
                    int tempId = ids[j];
                    ids[j] = ids[j + 1];
                    ids[j + 1] = tempId;

                    String tempName = names[j];
                    names[j] = names[j + 1];
                    names[j + 1] = tempName;

                    String tempDept = departments[j];
                    departments[j] = departments[j + 1];
                    departments[j + 1] = tempDept;

                    swapped = true;
                }
            }
            if (!swapped) break;
        }
    }

    public static int binarySearch(int[] ids, int targetId) {
        int low = 0, high = ids.length - 1;
        while (low <= high) {
            int mid = (low + high) / 2;
            if (ids[mid] == targetId) return mid;
            else if (ids[mid] < targetId) low = mid + 1;
            else high = mid - 1;
        }
        return -1;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of students: ");
        int n = sc.nextInt();
        sc.nextLine();

        int[] ids = new int[n];
        String[] names = new String[n];
        String[] departments = new String[n];

        for (int i = 0; i < n; i++) {
            System.out.println("\nEnter details for student " + (i + 1) + ":");
            System.out.print("ID: ");
            ids[i] = sc.nextInt();
            sc.nextLine();
            System.out.print("Name: ");
            names[i] = sc.nextLine();
            System.out.print("Department: ");
            departments[i] = sc.nextLine();
        }

        int choice;
        do {
            System.out.println("\n=== Student Search Menu ===");
            System.out.println("1. Linear Search");
            System.out.println("2. Binary Search");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            if (choice == 1 || choice == 2) {
                System.out.print("Enter student ID to search: ");
                int searchId = sc.nextInt();
                int index;
                
                if (choice == 1) {
                    index = linearSearch(ids, searchId);
                    System.out.println("\nResult (Linear Search):");
            } else {
                    sortById(ids, names, departments);
                    index = binarySearch(ids, searchId);
                    System.out.println("\nResult (Binary Search):");
                }

           if (index != -1) {
                    System.out.println("ID: " + ids[index] + ", Name: " + names[index] + ", Department: " + departments[index]);
            } else {
                    System.out.println("Student not found.");
                }
           } else if (choice != 3) {
                System.out.println("Invalid choice. Try again.");
            }
        } while (choice != 3);

        System.out.println("Exiting program.");
        sc.close();
    }
}
