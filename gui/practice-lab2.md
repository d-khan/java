# Practice lab 2 (This lab is not graded)

## Objective

Apply GUI in Java

## Prerequisite

Review the [GUI](https://htmlpreview.github.io/?https://github.com/d-khan/java/blob/main/gui/Lecture.html) lecture.

## Tasks

Modify the above program to allow the user to enter (or select) a dog's age in increments of 0.5. This requires changes to the spinner model and the stateChanged() method. In the stateChanged() method, make sure to use the appropriate data type for the spinner value (i.e., Double instead of Integer), and add more cases to the switch statement. You can use interpolation to determine the appropriate human age. For example, a dog age of 1.5 years results in a human age of (15 + 24) / 2 = 19.5 years.


```java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JSpinner;
import javax.swing.JTextField;
import javax.swing.SpinnerNumberModel;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ChangeListener;

public class DogYearsFrame extends JFrame implements ChangeListener {
    private JSpinner yearsSpinner;    // Triggers travel time calculation
    private JTextField ageHumanField; // Displays dog's age in human years
    private JLabel yearsLabel;        // Label for dog years
    private JLabel ageHumanLabel;     // Label for human years

    /* Constructor creates GUI components and adds GUI components
       using a GridBagLayout. */
    DogYearsFrame() {
        int initYear;     // Spinner initial value display
        int minYear;      // Spinner min value
        int maxYear;      // Spinner max value
        int stepVal;      // Spinner step

        initYear = 0;
        minYear = 0;
        maxYear = 30;
        stepVal = 1;

        // Used to specify GUI component layout
        GridBagConstraints layoutConst = null;

        // Specifies the types of values displayed in spinner
        SpinnerNumberModel spinnerModel = null;

        // Set frame's title
        setTitle("Dog's age in human years");

        // Create labels
        yearsLabel = new JLabel("Select dog's age (years):");
        ageHumanLabel = new JLabel("Age (human years):");

        // Create a spinner model, the spinner, and set the change listener
        spinnerModel = new SpinnerNumberModel(initYear, minYear, maxYear, stepVal);
        yearsSpinner = new JSpinner(spinnerModel);
        yearsSpinner.addChangeListener(this);

        // Create field
        ageHumanField = new JTextField(15);
        ageHumanField.setEditable(false);
        ageHumanField.setText("0 - 15");

        // Use a GridBagLayout
        setLayout(new GridBagLayout());

        // Specify component's grid location
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.anchor = GridBagConstraints.LINE_END;
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;
        add(yearsLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 10, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 1;
        layoutConst.gridy = 0;
        add(yearsSpinner, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.anchor = GridBagConstraints.LINE_END;
        layoutConst.gridx = 0;
        layoutConst.gridy = 1;
        add(ageHumanLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 10, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 1;
        layoutConst.gridy = 1;
        add(ageHumanField, layoutConst);
    }

    @Override
    public void stateChanged(ChangeEvent event) {
        Integer dogAgeYears;     // Dog age input

        dogAgeYears = (Integer) yearsSpinner.getValue();

        // Choose output based on dog's age component
        switch (dogAgeYears) {
            case 0:
                ageHumanField.setText("0 - 15");
                break;

            case 1:
                ageHumanField.setText("15");
                break;

            case 2:
                ageHumanField.setText("24");
                break;

            case 3:
                ageHumanField.setText("28");
                break;

            case 4:
                ageHumanField.setText("32");
                break;

            case 5:
                ageHumanField.setText("37");
                break;

            case 6:
                ageHumanField.setText("42");
                break;

            case 7:
                ageHumanField.setText("47");
                break;

            case 8:
                ageHumanField.setText("52");
                break;

            case 9:
                ageHumanField.setText("57");
                break;

            case 10:
                ageHumanField.setText("62");
                break;

            case 11:
                ageHumanField.setText("67");
                break;

            case 12:
                ageHumanField.setText("72");
                break;

            case 13:
                ageHumanField.setText("77");
                break;

            case 14:
                ageHumanField.setText("82");
                break;

            default:
                ageHumanField.setText("That's a long life!");
        }
    }

    /* Creates a DogYearsFrame and makes it visible */
    public static void main(String[] args) {
        // Creates DogYearsFrame and its components
        DogYearsFrame myFrame = new DogYearsFrame();

        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```
