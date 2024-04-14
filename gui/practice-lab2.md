# Practice lab 2 (This lab is not graded)

## Objective

Practice JButton in Java

## Prerequisite

Review the [GUI](https://github.com/d-khan/java/blob/main/gui/Lecture.md) lecture.

## Tasks

Write a program that takes user input (hourly wage) and displays output (yearly salary). You can assume 40 hours/week and 50 weeks/year for the yearly salary. Use two JButtons: ```Calculate``` to display the result and ```Reset``` to reset all the displays.
The display should look like this:

<p align="center">
<img src="https://github.com/d-khan/java/blob/main/gui/JButton.png" width=50% height=50%>
</p>

>### Solution (Do not look at the code below - try first)
&nbsp; &nbsp; &nbsp; 


<details>
  <summary>Are you really giving up to see the answer below???</summary>

```java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JTextField;

public class SalaryCalcButtonFrame extends JFrame implements ActionListener {
    private JLabel wageLabel;     // Label for hourly salary
    private JLabel salLabel;      // Label for yearly salary
    private JTextField salField;  // Displays hourly salary
    private JTextField wageField; // Displays yearly salary
    private JButton calcButton;   // Triggers salary calculation
    private JButton REcalcButton;

    /* Constructor creates GUI components and adds GUI components
       using a GridBagLayout. */
    SalaryCalcButtonFrame() {
        // Used to specify GUI component layout
        GridBagConstraints positionConst = null;

        // Set frame's title
        setTitle("Salary");

        // Set hourly and yearly salary labels
        wageLabel = new JLabel("Hourly wage:");
        salLabel = new JLabel("Yearly salary:");

        wageField = new JTextField(15);
        wageField.setEditable(true);
        wageField.setText("0");

        salField = new JTextField(15);
        salField.setEditable(false);

        // Create a "Calculate" button
        calcButton = new JButton("Calculate");
        REcalcButton = new JButton("Reset");

        // Use "this" class to handle button presses
        calcButton.addActionListener(this);

        REcalcButton.addActionListener(new ActionListener(){
            public void actionPerformed(ActionEvent ae){
                wageField.setText("0");
                salField.setText("0");
            }
        });

        // Use a GridBagLayout
        setLayout(new GridBagLayout());
        positionConst = new GridBagConstraints();

        // Specify component's grid location
        positionConst.gridx = 0;
        positionConst.gridy = 0;

        // 10 pixels of padding around component
        positionConst.insets = new Insets(10, 10, 10, 10);

        // Add component using the specified constraints
        add(wageLabel, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 0;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(wageField, positionConst);

        positionConst.gridx = 0;
        positionConst.gridy = 1;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(salLabel, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 1;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(salField, positionConst);

        positionConst.gridx = 0;
        positionConst.gridy = 2;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(calcButton, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 2;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(REcalcButton, positionConst);
    }

    /* Method is automatically called when an event
       occurs (e.g, button is pressed) */
    @Override
    public void actionPerformed(ActionEvent event) {
        String userInput;      // User specified hourly wage
        int hourlyWage;        // Hourly wage

        // Get user's wage input
        userInput = wageField.getText();

        // Convert from String to an integer
        hourlyWage = Integer.parseInt(userInput);

        // Display calculated salary
        salField.setText(Integer.toString(hourlyWage * 40 * 50)); //40 hours per week and 50 weeks per year
    }

    /* Creates a SalaryCalculatorFrame and makes it visible */
    public static void main(String[] args) {
        // Creates SalaryLabelFrame and its components
        SalaryCalcButtonFrame myFrame = new SalaryCalcButtonFrame();

        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```
</details>
