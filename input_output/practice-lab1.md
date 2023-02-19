# Practice lab (This lab is not graded)
## Objective
Reading from a string

## Task
Write code that uses the input string stream inSS to read input data from string userInput, and updates variables userMonth, userDate, and userYear. Sample output if the input is "Jan 12 1992":

## Input
Jan 12 1992

## Output
```
Month: Jan
Date: 12
Year: 1992
```

## Example code
```java
import java.util.Scanner;

public class StringInputStream {
    public static void main (String [] args) {
        Scanner scnr = new Scanner(System.in);
        Scanner inSS = null;
        String userInput;
        String userMonth;
        int userDate;
        int userYear;

        userInput = scnr.nextLine();
        inSS = new Scanner(userInput);
        userMonth = inSS.next();
        userDate = inSS.nextInt();
        userYear = inSS.nextInt();

        System.out.println("Month: " + userMonth);
        System.out.println("Date: " + userDate);
        System.out.println("Year: " + userYear);
    }
}
```
