# Inheritance

## Objective
Understand how subclasses and derived from the superclass.

## Pre-requisite
Review the "Inheritance" lecture before attending the lab. 

## Task
Assign courseStudent's name with Smith, age with 20, and ID with 9999. Use the printAll() member method and a separate println() statement to output courseStudents's data. 

## Partial code
```java
// ===== Code from file Person.java =====
public class Person {
   private int ageYears;
   private String lastName;

   public void setName(String userName) {
      lastName  = userName;
   }

   public void setAge(int numYears) {
      ageYears = numYears;
   }

   // Other parts omitted

   public void printAll() {
      System.out.print("Name: " + lastName);
      System.out.print(", Age: "  + ageYears);
   }
}
// ===== end =====

// ===== Code from file Student.java =====
public class Student extends Person {
   private int idNum;

   public void setID(int studentId) {
      idNum = studentId;
   }

   public int getID() {
      return idNum;
   }
}
// ===== end =====

// ===== Code from file StudentDerivationFromPerson.java =====
public class StudentDerivationFromPerson {
   public static void main(String[] args) {
      Student courseStudent = new Student();

      /* Your solution goes here  */

   }
}
// ===== end =====
```
## Expected output
```Name: Smith, Age: 20, ID: 9999```

## What to submit?
1. Draw a flowchart of your thought process. I found this [online flowchart website](http://www.draw.io) very useful. However, you can use any application of your choice. (2 marks).   
2. What were your challenges in performing the lab (from design to the implementation phases)? (2 mark).  
3. Create a video explaining how the code works. The video should show your face on one side of the screen preferably the top or bottom right of the screen. (1 mark)
4. Upload the working code. (5 marks)

## How to submit it?
Upload your work as a Markdown file to your GitHub account and share the link on Canvas. Please review the guide:"
[Submitting your assignments using Github](https://sdccd-edu.zoom.us/rec/share/SVvlngcEn-7CaNI8FvwEVJ5ulLp4sxpqN9hnCYvXeHHcls2e0TBlU47uATNklUf-.yX4fsJjsU2nuLGeX?startTime=1725121532000)"

## Deadline
The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric
- The video describes the code in detail. The code is working as per instruction, and the explanation of the questions is submitted (10 marks).  
- The video is submitted, and the code is working, but a partial explanation of the questions is submitted. (6+ marks).  
- The code is uploaded but not working regardless the video is submitted or not. (0 marks)
