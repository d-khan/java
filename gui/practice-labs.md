# Practice lab (This lab is not graded)

## Objective

Apply GUI in Java

## Prerequisite

Review the

## Tasks

Using the above FlyDriveFrame program, enter the input "31 and 32". Notice that the JFormattedTextField component only extracts the first valid number from this incorrectly formatted input string. Also, notice that the JFormattedTextField component automatically formats the displayed text when the user clicks on another component (e.g., the button).


```java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.NumberFormat;
import javax.swing.JButton;
import javax.swing.JFormattedTextField;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JTextField;

public class FlyDriveFrame extends JFrame implements ActionListener {
    private JButton calcButton;            // Triggers time calculation
    private JLabel distLabel;              // Label for distance input
    private JLabel hrsFlyLabel;            // Label for fly time
    private JLabel hrsDriveLabel;          // Label for drive time
    private JTextField hrsFlyField;        // Displays fly time
    private JTextField hrsDriveField;      // Displays drive time
    private JFormattedTextField distField; // Holds distance input

    /* Constructor creates GUI components and adds GUI components
       using a GridBagLayout. */
    FlyDriveFrame() {
        // Used to specify GUI component layout
        GridBagConstraints layoutConst = null;

        // Set frame's title
        setTitle("Fly Drive Travel Time Calculator");

        // Create labels
        distLabel = new JLabel("Distance (miles):");
        hrsFlyLabel = new JLabel("Flight time (hrs):");
        hrsDriveLabel = new JLabel("Driving time (hrs):");

        // Create button and add action listener
        calcButton = new JButton("Calculate");
        calcButton.addActionListener(this);

        // Create flight time filed
        hrsFlyField = new JTextField(15);
        hrsFlyField.setEditable(false);

        // Create driving time field
        hrsDriveField = new JTextField(15);
        hrsDriveField.setEditable(false);

        // Create and set-up an input field for numbers (not text)
        distField = new JFormattedTextField(NumberFormat.getNumberInstance());
        distField.setEditable(true);
        distField.setText("0");
        distField.setColumns(15); // Initial width of 10 units

        // Use a GridBagLayout
        setLayout(new GridBagLayout());

        // Specify component's grid location
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;
        add(distLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 10, 10);
        layoutConst.gridx = 1;
        layoutConst.gridy = 0;
        add(distField, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 5, 10, 10);
        layoutConst.gridx = 2;
        layoutConst.gridy = 0;
        add(calcButton, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 0, 1, 10);
        layoutConst.gridx = 1;
        layoutConst.gridy = 1;
        add(hrsFlyLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(1, 0, 10, 10);
        layoutConst.gridx = 1;
        layoutConst.gridy = 2;
        add(hrsFlyField, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 0, 1, 10);
        layoutConst.gridx = 2;
        layoutConst.gridy = 1;
        add(hrsDriveLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(1, 0, 10, 10);
        layoutConst.gridx = 2;
        layoutConst.gridy = 2;
        add(hrsDriveField, layoutConst);
    }

    /* Method is automatically called when an event
       occurs (e.g, Enter key is pressed) */
    @Override
    public void actionPerformed(ActionEvent event) {
        double totMiles;     // Distance to travel
        double hrsFly;       // Corresponding hours to fly
        double hrsDrive;     // Corresponding hours to drive

        // Get value from distance field
        totMiles = ((Number) distField.getValue()).doubleValue();

        // Check if miles input is positive
        if (totMiles >= 0.0) {
            hrsFly = totMiles / 500.0;
            hrsDrive = totMiles / 60.0;

            hrsFlyField.setText(Double.toString(hrsFly));
            hrsDriveField.setText(Double.toString(hrsDrive));
        }
        else {
            // Show failure dialog
            JOptionPane.showMessageDialog(this, "Enter a positive distance value!");
        }
    }

    /* Creates a FlyDriveFrame and makes it visible */
    public static void main(String[] args) {
        // Creates FlyDriveFrame and its components
        FlyDriveFrame myFrame = new FlyDriveFrame();

        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```
