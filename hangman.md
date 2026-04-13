# Hangman cheat sheet

## Load the file in Java and add data of the file into a string of an array

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

### Parse single element of an array

```java
String[] words = {"apple", "banana", "cat"};

for (String word : words) {
    System.out.println("Word: " + word);

    for (int i = 0; i < word.length(); i++) {
        char ch = word.charAt(i);
        System.out.println(ch);
    }

    System.out.println("----");
}
```

### Selecting a string from the Arraylist using Random
```java
import java.util.ArrayList;
import java.util.Random;

public class Main {
    public static void main(String[] args) {
        ArrayList<String> words = new ArrayList<>();
        words.add("apple");
        words.add("banana");
        words.add("cherry");
        words.add("mango");

        Random rand = new Random();
        int index = rand.nextInt(words.size()); // 0 to size-1

        String randomWord = words.get(index);
        System.out.println("Random word: " + randomWord);
    }
}
```
