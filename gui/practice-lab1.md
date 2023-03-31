# Practice lab (This lab is not graded)

## Objective

Apply Swing GUI components in Java

## Prerequisite

Review the [GUI](https://htmlpreview.github.io/?https://github.com/d-khan/java/blob/main/gui/Lecture.html) lecture.

## Tasks
Experiment the following code, and change the values,logical values and observe the output.

```java
import javax.swing.JFrame;
import javax.swing.JTextField;

public class SalaryGUI {
    public static void main(String[] args) {
        int hourlyWage;
        JFrame topFrame = null;        // Application window
        JTextField outputField = null; // Displays output salary

        hourlyWage = 20;

        // Create text field
        outputField = new JTextField();
        // Display program output using the text field
        outputField.setText("An hourly wage of " + hourlyWage + "/hr" +
                " yields $" + (hourlyWage * 40 * 50) + "/yr.");

        // Prevent user from editing output text
        outputField.setEditable(false);

        // Create window
        topFrame = new JFrame("Salary");

        // Add text field to window
        topFrame.add(outputField);

        // Resize window to fit components
        topFrame.pack();

        // Set program to terminate when window is closed
        topFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // Display window
        topFrame.setVisible(true);
    }
}

```
