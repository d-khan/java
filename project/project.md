# Project Activity: Insert data in mySQL from the tab-separated value file

## Objective

Automate the data insertion process in mySQL from the tab-separated value file using Java

## Make sure you go through the following items

- Review [Databases lecture](https://htmlpreview.github.io/?https://github.com/d-khan/java/blob/main/databases/Lecture.html).
- Perform [practice lab](https://github.com/d-khan/java/blob/main/databases/Practice-lab.md).
- Review [GUI lecture](https://github.com/d-khan/java/blob/main/gui/Lecture.md).
- Review [SQL cheat sheet](https://www.sqltutorial.org/sql-cheat-sheet/).

## Data set
- [Auto MPG data](https://github.com/d-khan/java/blob/main/project/auto-mpg.data-original)
- [Data set details](https://github.com/d-khan/java/blob/main/project/auto-mpg.names)

## Task
1. Create a database in mySQL called 'Auto'. **(2 marks)**
2. Using Java to insert data using SQL statements. The data is in tab separated value file, [Auto MPG data](https://github.com/d-khan/java/blob/main/project/auto-mpg.data-original), and the details about the data and data types can be found at [Data set details](https://github.com/d-khan/java/blob/main/project/auto-mpg.names). **(10 marks)**
3. Using GUI, create a text box which takes user input and another windows to display results. For example, if the text box says 'ALL' then you display the entire table. Under the hood, the corresponding SQL statement in Java will be running. **(4 marks)**
### Example
Be creative! You can use the following image as an example.
[See the example image](https://raw.githubusercontent.com/d-khan/java/refs/heads/main/project/Task3_project.png)

```sql
SELECT * from Auto
```
4. Use JSliders to create two sliders (MPG and horsepower). The user should select mpg and horsepower and the corresponding result will display. You need a WHERE clause to get the selected results. **(4 marks)**

### Example image
Be creative, you can use the following image as an example.
[See the example image](https://raw.githubusercontent.com/d-khan/java/refs/heads/main/project/Task4_project.png)

## What to submit?
  
1. What were your challenges in performing the lab (from design to the implementation phases)?
2. Submit all the codes and provide meaningful filenames.
3. Create a video that explains the working of the code. Furthermore, the video should show your face on one side of the screen (preferably the top or bottom right of the screen). Also, submit the code in the .java extension. 

## How to submit it?

- Upload your work in the .pdf or .txt format and clearly define your responses.  
- Use headings when possible. Upload the code in the .java or .txt extensions.
- Do not compress or zip files.

## Deadline

The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric

- The video describes each section clearly and the corresponding Java code and SQL statements are submitted. (100%)
- The video is submitted but not the code. (Score will be given based on the completed task).
- The code is uploaded but not working regardless the video is submitted or not. (0 marks)
