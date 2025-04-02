# lab6

student 

package assignments;
public class Student implements Comparable<Student> {
    private String firstName;
    private String lastName;
    private int testScore;

    public Student(String firstName, String lastName, int testScore) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.testScore = testScore;
    }

    public int getTestScore() {
        return testScore;
    }

    @Override
    public int compareTo(Student other) {
        // Sorting in descending order
        return Integer.compare(other.testScore, this.testScore);
    }

    @Override
    public String toString() {
        return firstName + " " + lastName + " - Score: " + testScore;
    }
}


sorting

package assignments;

public class Sorting {
    public static void selectionSort(Student[] students) {
        int n = students.length;
        for (int i = 0; i < n - 1; i++) {
            int maxIndex = i;
            for (int j = i + 1; j < n; j++) {
                if (students[j].compareTo(students[maxIndex]) < 0) {
                    maxIndex = j;
                }
            }
            // Swap elements
            Student temp = students[maxIndex];
            students[maxIndex] = students[i];
            students[i] = temp;
        }
    }
}


gradebook

package assignments;

public class Gradebook {
    private Student[] students;
    private int count;

    public Gradebook(int capacity) {
        students = new Student[capacity];
        count = 0;
    }

    public void addStudent(Student student) {
        if (count < students.length) {
            students[count++] = student;
        } else {
            System.out.println("Gradebook is full!");
        }
    }

    public void sortStudents() {
        Sorting.selectionSort(students);
    }

    public void printStudents() {
        for (Student student : students) {
            System.out.println(student);
        }
    }
}


driver

package assignments;

import java.util.Scanner;

public class driver {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Gradebook gradebook = new Gradebook(5);

        // Prompt user for student details
        for (int i = 0; i < 5; i++) {
            System.out.println("Enter details for student " + (i + 1));
            System.out.print("First Name: ");
            String firstName = scanner.next();
            System.out.print("Last Name: ");
            String lastName = scanner.next();
            int score;
            do {
                System.out.print("Test Score (0-100): ");
                score = scanner.nextInt();
            } while (score < 0 || score > 100);

            gradebook.addStudent(new Student(firstName, lastName, score));
        }

        // Sort students by test score in descending order
        gradebook.sortStudents();

        // Print sorted list
        System.out.println("\nSorted Student List:");
        gradebook.printStudents();

        scanner.close();
    }
}
