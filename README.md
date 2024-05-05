import java.util.ArrayList;
import java.util.Scanner;

// Task class to represent individual tasks
class Task {
    private String title;
    private String description;
    private String dueDate;
    private boolean completed;

    // Constructor
    public Task(String title, String description, String dueDate) {
        this.title = title;
        this.description = description;
        this.dueDate = dueDate;
        this.completed = false; // By default, task is not completed
    }

    // Getters and setters
    public String getTitle() {
        return title;
    }

    public String getDescription() {
        return description;
    }

    public String getDueDate() {
        return dueDate;
    }

    public boolean isCompleted() {
        return completed;
    }

    public void markAsComplete() {
        this.completed = true;
    }

    @Override
    public String toString() {
        return "Title: " + title + ", Description: " + description + ", Due Date: " + dueDate + ", Completed: " + completed;
    }
}

// Main class for the To-Do List application
public class ToDoListApp {
    private static ArrayList<Task> tasks = new ArrayList<>();
    private static Scanner scanner = new Scanner(System.in);

    // Main method to run the application
    public static void main(String[] args) {
        showMenu();
    }

    // Method to display the menu options
    private static void showMenu() {
        int choice;
        do {
            System.out.println("\n===== To-Do List Menu =====");
            System.out.println("1. Add Task");
            System.out.println("2. Mark Task as Complete");
            System.out.println("3. View Tasks");
            System.out.println("4. Remove Task");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline character

            switch (choice) {
                case 1:
                    addTask();
                    break;
                case 2:
                    markTaskAsComplete();
                    break;
                case 3:
                    viewTasks();
                    break;
                case 4:
                    removeTask();
                    break;
                case 5:
                    System.out.println("Exiting...");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 5);
    }

    // Method to add a new task
    private static void addTask() {
        System.out.println("\n===== Add Task =====");
        System.out.print("Enter task title: ");
        String title = scanner.nextLine();
        System.out.print("Enter task description: ");
        String description = scanner.nextLine();
        System.out.print("Enter due date: ");
        String dueDate = scanner.nextLine();

        Task newTask = new Task(title, description, dueDate);
        tasks.add(newTask);
        System.out.println("Task added successfully!");
    }

    // Method to mark a task as complete
    private static void markTaskAsComplete() {
        System.out.println("\n===== Mark Task as Complete =====");
        if (tasks.isEmpty()) {
            System.out.println("No tasks available.");
            return;
        }

        System.out.println("Select the task to mark as complete:");
        viewTasks();
        System.out.print("Enter task index: ");
        int index = scanner.nextInt();
        if (index >= 0 && index < tasks.size()) {
            Task task = tasks.get(index);
            task.markAsComplete();
            System.out.println("Task marked as complete.");
        } else {
            System.out.println("Invalid task index.");
        }
    }

    // Method to view all tasks
    private static void viewTasks() {
        System.out.println("\n===== View Tasks =====");
        if (tasks.isEmpty()) {
            System.out.println("No tasks available.");
            return;
        }

        for (int i = 0; i < tasks.size(); i++) {
            System.out.println("Task " + (i + 1) + ": " + tasks.get(i));
        }
    }

    // Method to remove a task
    private static void removeTask() {
        System.out.println("\n===== Remove Task =====");
        if (tasks.isEmpty()) {
            System.out.println("No tasks available.");
            return;
        }

        System.out.println("Select the task to remove:");
        viewTasks();
        System.out.print("Enter task index: ");
        int index = scanner.nextInt();
        if (index >= 0 && index < tasks.size()) {
            tasks.remove(index);
            System.out.println("Task removed successfully.");
        } else {
            System.out.println("Invalid task index.");
        }
    }
}
