``` java
import java.io.File;
import java.io.FileNotFoundException;
import java.util.ArrayList;
import java.util.Scanner;

public class ReadWords {
    public static void main(String[] args) {
        ArrayList<String> wordList = new ArrayList<>();

        try {
            File file = new File("words.txt"); // your file name
            Scanner scanner = new Scanner(file);

            // Read each word
            while (scanner.hasNext()) {
                String word = scanner.next();
                wordList.add(word);
            }

            scanner.close();

        } catch (FileNotFoundException e) {
            System.out.println("File not found.");
            return;
        }

        // Convert ArrayList to String array
        String[] words = wordList.toArray(new String[0]);

        // Test output
        for (String word : words) {
            System.out.println(word);
        }
    }
}
```
