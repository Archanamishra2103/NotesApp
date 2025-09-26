# NotesApp
A simple console-based Notes Manager built in Java using File I/O. The app allows users to write and save notes to a file, and read them later directly from the terminal.


    import java.io.*;
    import java.util.Scanner;

    public class NotesApp {
    private static final String FILE_NAME = "notes.txt";

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\n--- Notes App ---");
            System.out.println("1. Write a new note");
            System.out.println("2. View all notes");
            System.out.println("3. Exit");
            System.out.print("Enter choice: ");
            choice = sc.nextInt();
            sc.nextLine(); // consume newline

            switch (choice) {
                case 1 -> writeNote(sc);
                case 2 -> readNotes();
                case 3 -> System.out.println("Exiting... Goodbye!");
                default -> System.out.println("Invalid choice, try again.");
            }
        } while (choice != 3);

        sc.close();
    }

    private static void writeNote(Scanner sc) {
        try (FileWriter fw = new FileWriter(FILE_NAME, true)) {
            System.out.print("Enter your note: ");
            String note = sc.nextLine();
            fw.write(note + System.lineSeparator());
            System.out.println("Note saved successfully!");
        } catch (IOException e) {
            System.out.println("Error writing note: " + e.getMessage());
        }
    }

    private static void readNotes() {
        try (BufferedReader br = new BufferedReader(new FileReader(FILE_NAME))) {
            String line;
            System.out.println("\n--- Saved Notes ---");
            while ((line = br.readLine()) != null) {
                System.out.println("- " + line);
            }
        } catch (FileNotFoundException e) {
            System.out.println("No notes found yet. Write one first!");
        } catch (IOException e) {
            System.out.println("Error reading notes: " + e.getMessage());
        }
    }
    }
