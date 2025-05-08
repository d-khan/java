# Java database programming

## What is a database system

A database management system (or DBMS) is essentially nothing more than a computerized data-keeping system. Users of the system are given facilities to perform several kinds of operations on such a system for either manipulating the data in the database or managing the database structure itself.

<img width="476" alt="image" src="https://user-images.githubusercontent.com/11669149/229358799-cc16b3ce-8271-4cc1-bf10-1e54569e10ee.png">

## What is a Relational Database (RDBMS)?

A relational database is a type of database that stores and provides access to data points that are related to one another. Relational [databases](https://www.oracle.com/database/what-is-database/) are based on the relational model, an intuitive, straightforward way of representing data in tables. In a relational database, each row in the table is a record with a unique ID called the key. The columns of the table hold attributes of the data, and each record usually has a value for each attribute, making it easy to establish relationships among data points.

**Course table**

<img width="692" alt="image" src="https://user-images.githubusercontent.com/11669149/229359283-8008d495-2e42-4a36-85ac-26997b8275d7.png">

**Student table**

<img width="722" alt="image" src="https://user-images.githubusercontent.com/11669149/229359325-c6ffc6ae-329a-42a4-a0af-16a4219bcd22.png">

**Enrollment table**

<img width="490" alt="image" src="https://user-images.githubusercontent.com/11669149/229359423-c931fc81-78cf-4566-8a7e-9700f60beb4b.png">

> **Table vs file**
>
> A table or a relation is not same as a file. Most of the relational database systems store multiple tables in a file.

## Integrity constants

An integrity constraint imposes a condition that all legal instances of the relations must satisfy. In general, there are three types of constraints: ***domain constraint, primary key constraint***, and ***foreign key constraint***. Domain constraints and primary key constraints are known as ***intra-relational constraints***, meaning that a constraint involves only one relation. The foreign key constraint is known as ***inter-relational***, meaning that a constraint involves more than one relation.

### Domain constraints

<img width="711" alt="image" src="https://user-images.githubusercontent.com/11669149/229359611-4baa536a-4ba0-4b8f-a5b1-1b0428945188.png">

#### Example

The code below is written in SQL language.

```sql
create table Course (
  courseId char(5),
  subjectId char(4) not null, 
  courseNumber integer, 
  title varchar(50) not null, 
  numOfCredits integer, 
  constraint greaterThanOne 
       check (numOfCredits >= 1));
```

### Primary key constraints

The *primary key constraint* specifies that the primary key value of a tuple cannot be null and no two tuples in the relation can have the same value on the primary key. The DBMS enforces the primary key constraint. For example, if you attempt to insert a record with the same primary key as an existing record in the table, the DBMS would report an error and reject the operation. 

#### Example

The *primary* key is one of the candidate keys designated by the database designer. The primary key is often used to identify tuples in a relation.

```sql
create table Course (
  courseId char(5),
  subjectId char(4) not null, 
  courseNumber integer, 
  title varchar(50) not null, 
  numOfCredits integer, 
  primary key (courseId)
);
```

### Foreign key constraints

In a relational database, data are related. Tuples in a relation are related and tuples in different relations are related through their common attributes. Informally speaking, the common attributes are foreign keys. The *foreign key constraints* define the relationships among relations. 

<img width="721" alt="image" src="https://user-images.githubusercontent.com/11669149/229403624-3cf64416-3f1d-42d7-8dab-7f20697913b2.png">

```sql
create table Enrollment (
  ssn char(9), 
  courseId char(5),
  dateRegistered date,  
  grade char(1),
  primary key (ssn, courseId),
  foreign key (ssn) references Student,
  foreign key (courseId) references Course
); 
```

## Structured Query Language (SQL)

> **Note: This section has a video that is available in Canvas**

To access or write applications for database systems, you need to use the Structured Query Language (SQL). SQL is the universal language for accessing relational database systems. Application programs may allow users to access database without directly using SQL, but these applications themselves must use SQL to access the database.

> **Note: Before attempting the following commands, ensure you have installed a SQL server and the server is running. Take a look on the video posted in Canvas**

### Examples of simple SQL statements

#### Connect to the SQL server. Use mySQL shell.
Make sure the prompt says SQL on the left hand side. If it does not, then type ```\sql```.
```
\connect root@localhost:3306
```
#### Log in to your MySQL Server (as root) from the command prompt

```
mysql -u root -p
```



Then enter your MySQL root password. It is not set by default, so all you need to do is press the [Enter] key if you never set it. 

#### Display users in MySQL Server

``` sql
select distinct user from mysql.user;
```

<img width="411" alt="image" src="https://user-images.githubusercontent.com/11669149/229417292-1af08d8b-80cb-4708-b72a-a67ee9b37b9f.png">

#### Create users

```sql
create user 'testuser'@'localhost' identified by 'Pa$$word';
```

<img width="625" alt="image" src="https://user-images.githubusercontent.com/11669149/229423253-4c3ea472-879e-40bb-abd3-6ad94306f78e.png">

<img width="416" alt="image" src="https://user-images.githubusercontent.com/11669149/229423868-2ab7defc-6a31-46d7-bc87-04462737e242.png">

#### Grant permissions (giving root permission to the user)

```sql
grant all privileges on *.* to 'testuser'@'localhost';
```

<img width="557" alt="image" src="https://user-images.githubusercontent.com/11669149/229426204-0a199d71-7974-4486-a9d9-a7264344986a.png">

Exit from the sql prompt by typing `exit`.

At the command prompt, type the following command to enter into sql using a user **testuser**.

`mysql -u testuser -p`

#### Check which user is connected

```sql
select user();
```

<img width="232" alt="image" src="https://user-images.githubusercontent.com/11669149/229426676-a12d95c9-2afb-4792-a760-cc1aab1a35cd.png">

#### Create and select database

```sql
create database testdb;
use testdb;
```

#### Create table Course

```sql
create table Course (
  courseId char(5),
  subjectId char(4) not null, 
  courseNumber integer, 
  title varchar(50) not null, 
  numOfCredits integer, 
  primary key (courseId)
);
```

<img width="373" alt="image" src="https://user-images.githubusercontent.com/11669149/229410668-e968a01c-2d1f-44ae-8314-d150ae449532.png">

#### Create table Student

```sql
create table Student (
  ssn char(9), 
  firstName varchar(25), 
  mi char(1), 
  lastName varchar(25), 
  birthDate date,  
  street varchar(25),  
  phone char(11),  
  zipCode char(5),
  deptId char(4),  
  primary key (ssn)
); 
```

<img width="344" alt="image" src="https://user-images.githubusercontent.com/11669149/229410780-eceee3a1-6716-4e86-8dab-a9227036113b.png">

#### Show table fields and data types

```sql
describe Course;
```

<img width="571" alt="image" src="https://user-images.githubusercontent.com/11669149/229410988-1aa97f9d-a6de-4f52-a725-1de8cf1ce719.png">

#### Insert records into the Course table

```sql
insert into Course (courseId, subjectId, courseNumber, title, numOfCredits) 
values ('11113', 'CSCI', '3720', 'Database Systems', 3);
```

<img width="758" alt="image" src="https://user-images.githubusercontent.com/11669149/229411070-25eeb62f-9285-46f5-b645-9ab7a54e7db1.png">

#### Select records from the Course table

```sql
select * from Course;
```

<img width="680" alt="image" src="https://user-images.githubusercontent.com/11669149/229411191-0b94cfa6-1fc2-42f0-97a8-088b9c9eb296.png">

#### Update records in the Course table

```sql
update course
set numofcredits = 4
where courseID = '11113';
```

<img width="678" alt="image" src="https://user-images.githubusercontent.com/11669149/229412968-4a5b9973-b624-40ca-8cbc-40e2d08f4a37.png">

#### Delete a record in the Course table

```sql
delete from Course where courseid = '11113';
```

<img width="495" alt="image" src="https://user-images.githubusercontent.com/11669149/229414632-ed198837-d718-46b7-b825-3db59372fb28.png">

#### Delete an entire database

```sql
drop database testdb;
```

### Why Java for Database Programming?

- First, Java is platform independent. You can develop platform-independent database applications using SQL and Java for any relational database systems. 

- Second, the support for accessing database systems from Java is built into Java API, so you can create database applications using all Java code with a common interface. 

<img width="578" alt="image" src="https://user-images.githubusercontent.com/11669149/229419395-785ddfca-09fa-4c53-910b-7dceac4d7b89.png">

> **Note: Before running the following code, ensure that the user, database, and tables have been created and the table has at least one record, as EXACTLY mentioned in the above-mentioned steps.**
>
> **Secondly, the correct J connector file according to the OS is downloaded.**

**Simplejdbc.java**

```java
import java.sql.*;
public class SimpleJdbc {
  public static void main(String[] args)
      throws SQLException, ClassNotFoundException {
    // Load the JDBC driver
    Class.forName("com.mysql.cj.jdbc.Driver");
    System.out.println("Driver loaded");
    
    // Establish a connection
    // Assuming the database name is 'testdb', user is 'testuser'
    // and password is 'Pa$$word'
    Connection connection = DriverManager.getConnection
      ("jdbc:mysql://localhost/testdb","testuser","Pa$$word");
    System.out.println("Database connected");
    
    // Create a statement
    Statement statement = connection.createStatement();
    
    // Execute a statement
    ResultSet resultSet = statement.executeQuery
      ("select * from Course;");
      
      // Iterate through the result and print the student names
    while (resultSet.next())
      System.out.println(resultSet.getString(1) + "\t" +
        resultSet.getString(2) + "\t" + resultSet.getString(3) + "\t" +
        resultSet.getString(4) + "\t" + resultSet.getString(5));
    
    // Close the connection
    connection.close();
  }
}
```

**Ensure the Java connector and the above file are in the same folder. Run the following command at the command prompt.**

`java -cp mysql-connector-j-8.0.32.jar Simplejdbc.java`

<img width="855" alt="image" src="https://user-images.githubusercontent.com/11669149/229436319-1c9cfcfc-3c7f-46ae-91a8-e5b38b594a81.png">

## Conclusion

- A relational database is a type of database that stores and provides access to data points that are related to one another. 
- In a relational database, each row in the table is a record with a unique ID called the key. The columns of the table hold attributes of the data, and each record usually has a value for each attribute, making it easy to establish relationships among data points.
- To access or write applications for database systems, you need to use the Structured Query Language (SQL). 
- J connector allows access to SQL server within the Java programming environment.
