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
