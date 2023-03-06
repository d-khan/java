# Overriding methods

## Objective
Understand how to use overriding methods.

## Pre-requisite
Review the "Inheritance" lecture before attending the lab. 

## Task
- Write main() and a base `Book` class, define a derived class called `Encyclopedia` with member methods to get and set private fields of the following types:

  - String to store the edition
  - int to store the number of pages

  Within the derived `Encyclopedia` class, define a printInfo() method that overrides the `Book` class' printInfo() method by printing the title, author, publisher, publication date, edition, and number of pages.

## Expected input
```
The Hobbit
J. R. R. Tolkien
George Allen & Unwin
21 September 1937
The Illustrated Encyclopedia of the Universe
Ian Ridpath
Watson-Guptill
2001
2nd
384
```
## Expected output
```Course Information:
CBook Information: 
   Book Title: The Hobbit
   Author: J. R. R. Tolkien
   Publisher: George Allen & Unwin
   Publication Date: 21 September 1937
Book Information: 
   Book Title: The Illustrated Encyclopedia of the Universe
   Author: Ian Ridpath
   Publisher: Watson-Guptill
   Publication Date: 2001
   Edition: 2nd
   Number of Pages: 384
```
## What to submit?
1. Draw a flowchart of your thought process. I found this [online flowchart website](http://www.draw.io) very useful. However, you can use any application of your choice. **(2 marks).**   
2. What were your challenges in performing the lab (from design to the implementation phases)? **(2 marks)**.  
3. Create a video that explains the working of the code. Furthermore, the video should show your face on one side of the screen (preferably the top or bottom right of the screen). Also, submit the code in the .java extension. **(6 marks)**

## How to submit it?
- Upload your work in the .pdf or .txt format and clearly define your responses.  
- Use headings when possible. Upload the code in the .java extension.
- Do not compress or zip files.

## Deadline
The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric
- The video describes the code in detail. The code is working as per instruction, and the explanation of the questions is submitted (10 marks).  
- The video is submitted, and the code is working, but a partial explanation of the questions is submitted. (6+ marks).  
- The code is uploaded but not working regardless the video is submitted or not. (0 marks)
