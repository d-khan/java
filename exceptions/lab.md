# Activity: Exceptions

## Objective

Create Step counter exceptions

## Pre-requisite

Review the "Exceptions" lecture before attending the lab. 

## Task

A pedometer treats walking 2,000 steps as walking 1 mile. Write a stepsToMiles() method that takes the number of steps as an integer parameter and returns the miles walked as a double. The stepsToMiles() method throws an Exception object with the message "Exception: Negative step count entered." when the number of steps is negative. Complete the main() method that reads the number of steps from a user, calls the stepsToMiles() method, and outputs the returned value from the stepsToMiles() method. Use a try-catch block to catch any Exception object thrown by the stepsToMiles() method and output the exception message.

Output each floating-point value with two digits after the decimal point, which can be achieved as follows:
`System.out.printf("%.2f", yourValue);`

__Expected input__

```
5345
```

__Expected output__

```Course Information:
2.67
```

**Expected input**

```
-3850
```

**Expected output**

```
Exception: Negative step count entered.
```

## What to submit?

1. Draw a flowchart of your thought process. I found this [online flowchart website](http://www.draw.io) very useful. However, you can use any application of your choice. (2 marks).  
2. What were your challenges in performing the lab (from design to the implementation phases)? (2 marks).  
3. Create a video explaining how the code works. The video should show your face on one side of the screen preferably the top or bottom right of the screen. (1 mark)
4. Upload the working code. (5 marks)

## How to submit it?
Upload your work to your Github account and share the link on Canvas.

## Deadline

The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric

- The video describes the code in detail. The code is working as per instruction, and the explanation of the questions is submitted (10 marks).  
- The video is submitted, and the code is working, but a partial explanation of the questions is submitted. (6+ marks).  
- The code is uploaded but not working regardless the video is submitted or not. (0 marks)
