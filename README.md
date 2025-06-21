package fileoperations;
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class Fileoperations {

    private static final String FILE_PATH = "example.txt";

    public static void main(String[] args) {
        // Write to a file
        writeToFile("Hello, World!\nThis is a sample text file.");

        // Read from a file
        readFromFile();

        // Modify the file
        modifyFile("World", "Java");
        
        // Read the modified file
        readFromFile();
    }

    // Method to write to a file
    public static void writeToFile(String content) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(FILE_PATH))) {
            writer.write(content);
            System.out.println("Data written to file successfully.");
        } catch (IOException e) {
            System.err.println("Error writing to file: " + e.getMessage());
        }
    }

    // Method to read from a file
    public static void readFromFile() {
        try (BufferedReader reader = new BufferedReader(new FileReader(FILE_PATH))) {
            String line;
            System.out.println("Reading from file:");
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.err.println("Error reading from file: " + e.getMessage());
        }
    }

    // Method to modify the file
    public static void modifyFile(String oldString, String newString) {
        try {
            String content = new String(Files.readAllBytes(Paths.get(FILE_PATH)));
            content = content.replace(oldString, newString);
            writeToFile(content);
            System.out.println("File modified successfully.");
        } catch (IOException e) {
            System.err.println("Error modifying file: " + e.getMessage());
        }
    }
}
