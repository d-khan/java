# Graphical User Interface

## Basic graphics

- Java supports a set of objects for developing graphical applications. A **graphical application** is a program that displays drawings and other graphical objects. Graphical applications display their contents inside a window called a **frame** using a **JFrame** object. The following program shows how to create and configure a JFrame object to display an empty application window.

### Example - Creating a JFrame object for a graphical application.

``` java
import javax.swing.JFrame;

public class EmptyFrame {
   public static void main(String[] args) {
      
      // Construct the JFrame object
      JFrame appFrame = new JFrame();

      // Set the frame's width (400) and height (250) in pixels
      appFrame.setSize(400, 250);
      
      // Set the frame's title
      appFrame.setTitle("An Empty Frame");
      
      // Set the program to exit when the user
      // closes the frame
      appFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
      
      // Make the frame visible to the user
      appFrame.setVisible(true);
   }
}
```

<img width="414" alt="image" src="https://user-images.githubusercontent.com/11669149/228693771-678385af-1ffb-4b17-a31e-cce7a05ed745.png">

Constructing a JFrame object does not immediately display a frame. The program uses the methods supported by the JFrame object to configure and display the frame as follows:

1. **Set the frame's size** by calling the setSize() method with arguments for the width and height, as in `appFrame.setSize(400, 250)`. Forgetting to set the frame's size results in a frame too small to see.
2. **Set the frame's title** by calling the setTitle() method with a String as the argument. Alternatively, the frame's title can be provided as an argument to JFrame's constructor as in `JFrame appFrame = new JFrame("An Empty Frame")`.
3. **Set the frame's closing operation** by calling the setDefaultCloseOperation() method, as in `appFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE)`. This statement configures the program to exit when the user closes the frame.
4. **Make the frame visible** to the user by calling the setVisible() method with a boolean argument of true.

A JFrame can be used to draw graphical objects, such as rectangles, circles, and lines. To display graphical objects, a programmer can add a *custom* JComponent object to a frame. A **JComponent** is a blank graphical component that a programmer extends (or customizes) with custom code in order to draw basic shapes.

The following program demonstrates how to create a custom class that extends JComponent to draw 2D graphics. Creating a class that extends JComponent involves advanced topics, including defining a class and inheritance, which are discussed elsewhere. For now, the following class can be used as a template.

### Example - Drawing a histogram in a frame

**HistogramComponent.java**

``` java
import java.awt.Color;
import java.awt.Graphics;
import java.awt.Graphics2D;
import java.awt.Rectangle;
import javax.swing.JComponent;

// HistogramComponent extends the functionality of a JComponent
// in order to draw a histogram.
public class HistogramComponent extends JComponent {
   
   // Paints a histogram with three bins
   @Override
   public void paintComponent(Graphics g) {  
      // Cast to Graphics2D
      Graphics2D graphicsObj = (Graphics2D) g;
      
      // Draw 1st bin as an olive colored rectangle at (10,10)
      // with width = 200 and height = 50
      Rectangle binRectangle1 = new Rectangle(10, 10, 200, 50); 
      Color binColor1 = new Color(128, 128, 0);
      graphicsObj.setColor(binColor1);
      graphicsObj.fill(binRectangle1);
      
      // Draw 2nd bin as a teal blue rectangle at (10,75)
      // with width = 150 and height = 50
      Rectangle binRectangle2 = new Rectangle(10, 75, 150, 50); 
      Color binColor2 = new Color(0, 200, 200);
      graphicsObj.setColor(binColor2);
      graphicsObj.fill(binRectangle2);
      
      // Draw 3rd bin as a gray rectangle at (10,140)
      // with width = 350 and height = 50
      Rectangle binRectangle3 = new Rectangle(10, 140, 350, 50); 
      Color binColor3 = new Color(100, 100, 100);
      graphicsObj.setColor(binColor3);
      graphicsObj.fill(binRectangle3);
   }
}
```

**HistogramViewer.java**

```java
import javax.swing.JFrame;

public class HistogramViewer {
   public static void main(String[] args) {
      JFrame appFrame = new JFrame();
      HistogramComponent histogramComponent = new HistogramComponent();

      appFrame.setSize(400, 250);
      appFrame.setTitle("Histogram Viewer");
      appFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
      
      // Add the HistogramComponent object to the frame
      appFrame.add(histogramComponent);
      
      // Set the frame and its contents visible
      appFrame.setVisible(true);
   }
}
```

<img width="393" alt="image" src="https://user-images.githubusercontent.com/11669149/228694473-f6387c80-505f-4c56-9d20-09d77095dc2b.png">

The program first creates a HistogramComponent object named histogramComponent and adds the object to the JFrame object using the add() method. Once added, the JFrame automatically calls the histogramComponent objects paintComponent() method whenever the JFrame object is updated, such as when the frame is resized.

The HistogramComponent's paintComponent() uses Rectangle and Color objects to draw a simple histogram with three bins, using the operations:

1. **Cast the Graphics object to Graphics2D**: The statement `Graphics2D graphicsObj = (Graphics2D) g;` converts the original Graphics object argument to a graphics object that supports drawing two-dimensional objects.
2. **Create a Rectangle object**: A **Rectangle** object stores the location and size of a rectangle shape. A Rectangle's constructor accepts arguments for location and size (in pixel units) as specified by the constructor definition: `Rectangle(int x, int y, int width, int height)`.
3. **Create a Color object**: A **Color** object represents a color in the red, green, blue color space. A Color constructor accepts an integer value between 0 to 255 for each color channel as specified by the constructor definition: `Color(int red, int green, int blue)`. For example, the statement `Color binColor1 = new Color(128, 128, 0);` creates a Color object with an olive color.
4. **Set the color used by the Graphics2D object**: Graphic2D's setColor() method sets the color that the Graphics2D object will use for subsequent drawing operations.
5. **Draw the shape**: A Graphic2D object provides different methods for drawing shapes. The draw() method will draw an outline of a shape, such as a Rectangle object, using the Graphic2D object's current color. The fill() method will draw a shape filling the interior of the shape with the Graphic2D object's current color.

## Introduction to graphical user interfaces

- Java supports a set of components, called **Swing GUI components**, for developing custom GUIs.
- A GUI, or **graphical user interface**, enables the user to interface with a program via the use of graphical components such as windows, buttons, text boxes, etc. as opposed to text-based interfaces like the traditional command line. 
- The following example calculates a yearly salary based on an hourly wage and utilizes Swing GUI components in order to create a GUI that displays the program's output.

### Example - displaying a yearly salary using a GUI

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

<img width="393" alt="Screen Shot 2023-03-29 at 9 08 30 PM" src="https://user-images.githubusercontent.com/11669149/228726719-e4c8bbbc-ce69-4ce0-a478-0900342400bb.png">

- The above program utilizes two basic Swing GUI components: **JTextField** and **JFrame**. The resulting GUI consists of a window (i.e., a JFrame) and a text field (i.e., a JTextField), as illustrated by the screenshot above.
- A JTextField is a Swing GUI component that enables a programmer to display a line of text and is available via the import statement `import javax.swing.JTextField;`.
- The statement `outputField = new JTextField();` creates a JTextField object, which is represented by the variable outputField.
- A programmer can then use JTextField's setText() method to specify the text that will be displayed, as in the statement `outputField.setText("An hourly ... ");`. 
- By default, a JTextField allows users to modify the displayed text at runtime for the purposes of input (discussed elsewhere). However, the above program invokes JTextField's setEditable() method with the boolean literal false, as in `outputField.setEditable(false);`, to prevent users from editing the displayed text.
- A JFrame is a **top-level container** of GUI components and serves as the application's main window. 
- The JFrame class is available to programmers via the import statement `import javax.swing.JFrame;`. The statement `frame = new JFrame("Salary");` creates a window frame titled "Salary", as specified by the String literal within parentheses.
- A frame must contain all GUI components that should be visible to the user. A programmer uses JFrame's add() method to add GUI components to the frame. For example, the statement `frame.add(outputField);` adds the JTextField component, outputField, to the frame. The outputField text field is contained within the frame and displayed within the application's window.

- After adding all GUI components to a frame, a programmer then invokes JFrame's pack() method, as in `frame.pack();`, to automatically resize the frame to fit all of the contained components. Importantly, the pack() method resizes the window according to the current state of the contained components. Thus, modifying, adding, or removing GUI components after the call to pack() may result in a window that is not sized appropriately.

JFrame's pack() method uses the preferred size of its contained components in order to determine the appropriate size for the window. Try removing the statement frame.pack() from the above program and observe the effect. Notice how the window no longer displays the entire text of the JTextField component. Instead, the window defaults to a default size without considering the size of the frame's contained components.

Now restore the program to the original state and try moving the statement `outputField.setText("An hourly wage ...");` after the call to pack() (i.e., after the statement frame.pack();). Run the program once again and observe the output. Although the program invoked the pack() method, the text field is not displayed properly within the window. The statement order matters. The pack() method resizes the window according to the current state of the frame's components. Thus, changing the amount of text displayed by a JTextField component after the call to pack() will not automatically resize the window in order to fit the text. 

- By default, closing a GUI window does not terminate the program. Thus, the statement `frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);` is required so that the program terminates properly when the GUI window is closed. Lastly, the statement `frame.setVisible(true);` makes the frame visible on the screen.

In summary, the statements in the program's main() method construct a GUI as outlined by the following procedure:

1. Create GUI components (e.g., JTextField)
2. Create a top-level GUI component container (e.g., JFrame)
3. Add GUI components to the top-level container
4. Configure the top-level container (e.g., set the default close operation)
5. Display the top-level container (e.g., make the frame visible)

## Positioning GUI components using a GridBagLayout

- A **layout manager** affords programmers control over the positioning and layout of GUI components within a JFrame or other such containers.
- A **GridBagLayout** positions GUI components in a two-dimensional grid and is one of the layout managers supported by Java.

### Example - Using a GridBagLayout to arrange GUI components

```java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JTextField;

public class SalaryLabelGUI {

    public static void main(String[] args) {
        int hourlyWage;
        JFrame topFrame = null;                // Application window
        JLabel wageLabel = null;               // Label for hourly salary
        JLabel salLabel = null;                // Label for yearly salary
        JTextField salField = null;            // Displays hourly salary
        JTextField wageField = null;           // Displays yearly salary
        GridBagConstraints layoutConst = null; // GUI component layout

        hourlyWage = 20;

        // Set hourly and yearly salary
        wageLabel = new JLabel("Hourly wage:");
        salLabel = new JLabel("Yearly salary:");

        wageField = new JTextField(15);
        wageField.setEditable(false);
        wageField.setText(Integer.toString(hourlyWage));

        salField = new JTextField(15);
        salField.setEditable(false);
        salField.setText(Integer.toString((hourlyWage * 40 * 50)));

        // Create frame and add components using GridBagLayout
        topFrame = new JFrame("Salary");

        // Use a GridBagLayout
        topFrame.setLayout(new GridBagLayout());

        // Create GridBagConstraints
        layoutConst = new GridBagConstraints();

        // Specify component's grid location
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;

        // 10 pixels of padding around component
        layoutConst.insets = new Insets(10, 10, 10, 10);

        // Add component using the specified constraints
        topFrame.add(wageLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.gridx = 1;
        layoutConst.gridy = 0;
        layoutConst.insets = new Insets(10, 10, 10, 10);
        topFrame.add(wageField, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.gridx = 0;
        layoutConst.gridy = 1;
        layoutConst.insets = new Insets(10, 10, 10, 10);
        topFrame.add(salLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.gridx = 1;
        layoutConst.gridy = 1;
        layoutConst.insets = new Insets(10, 10, 10, 10);
        topFrame.add(salField, layoutConst);

        // Terminate program when window closes
        topFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // Resize window to fit components
        topFrame.pack();

        // Display window
        topFrame.setVisible(true);
    }
}
```

<img width="425" alt="Screen Shot 2023-03-30 at 7 27 23 AM" src="https://user-images.githubusercontent.com/11669149/228868595-8db890e2-8307-48ba-84c7-fb705fc8576d.png">

The above program displays an hourly wage and a yearly salary using the JTextField component's wageField and salaryField respectively. The statements creating the JTextField components (e.g., `wageField = new JTextField(15);`) now specify the fields' widths in number of columns, where a column is proportional to a character's pixel width given a particular font.

Additionally, the program contains two JLabel Swing GUI components, which allow programmers to display text that is typically used for the purposes of describing, or labeling, other GUI components. For example, the statement `wageLabel = new JLabel("Hourly wage:");` creates a JLabel component that describes the value displayed in the wageField. The JLabel class is available to programmers via the import statement `import javax.swing.JLabel;`.

Because the above program uses more than one Swing GUI component, a layout manager is necessary in order to specify the relative position of each component within the frame. A GridBagLayout is a layout manager that allows programmers to place components in individual cells within a two-dimensional grid. Each cell of this grid is indexed using one number for the column, x, and another number for the row, y. The top-left cell is at location (x=0, y=0), and column numbers increase going right, while row numbers increase going down. The programmer is additionally able to add padding (i.e., empty space) between Swing GUI components in order to make the GUI easier to understand as well as more aesthetically pleasing. The following animation illustrates the process of specifying the layout for each GUI component.

<img width="618" alt="image" src="https://user-images.githubusercontent.com/11669149/228870981-e463687c-f230-41f7-a1d6-f9dbbf02d99e.png">

<img width="640" alt="image" src="https://user-images.githubusercontent.com/11669149/228871112-19adebff-1d48-4991-a89f-a7e1c1c5a8ef.png">

<img width="667" alt="image" src="https://user-images.githubusercontent.com/11669149/228871313-19c84dbb-de34-4ceb-8840-ae12c7f39900.png">

<img width="659" alt="image" src="https://user-images.githubusercontent.com/11669149/228871606-dee29fd7-617a-4195-867e-9e6ac7b27ffe.png">

<img width="660" alt="image" src="https://user-images.githubusercontent.com/11669149/228871753-95bb788c-84ee-4804-8fac-5f8f8f9922ec.png">

<img width="663" alt="image" src="https://user-images.githubusercontent.com/11669149/228871875-fae24e36-aea3-4001-a3fb-1e3dfe156b03.png">


<img width="629" alt="Screen Shot 2023-03-30 at 12 34 58 PM" src="https://user-images.githubusercontent.com/11669149/228944833-848305ed-54d4-4d87-85fa-401444f81e79.png">


