# Practice lab (This lab is not graded)

## Objective

Create database, insert record in the table using SQL.

## Prerequisite

Review the [Databases](https://htmlpreview.github.io/?https://github.com/d-khan/java/blob/main/databases/Lecture.html) lecture.

## Tasks
- Use testuser account. The account creation steps and privileges are already mentioned in the lecture.
- Create a database called __Miramar__; create a table called __Student__' and add the following record

- ssn, firstname, middlename, lastname, birthday, street, phone, zipcode, deptid
- where ssn is a primary key.

## Steps
1. Make sure you are in the correct user account __testuser__.
```sql
select user();
```
<img width="218" alt="image" src="https://user-images.githubusercontent.com/11669149/229569059-5c62f1bd-1d6c-40ed-a471-1ea07a3b5aea.png">

2. Create the database __Miramar__.
```sql
create database Miramar;
```
<img width="332" alt="image" src="https://user-images.githubusercontent.com/11669149/229569741-9e6d5986-9758-4257-a1f7-bbf2f00cd67e.png">

3. Use the database __Miramar__
```sql
use Miramar;
```

4. Create the table __Student__
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
<img width="354" alt="image" src="https://user-images.githubusercontent.com/11669149/229570148-9018d3a6-92e8-46b9-87ee-533549ceac80.png">

5. Very that the table is created and all the data types are correctly defined.
```sql
describe course;
```
<img width="539" alt="image" src="https://user-images.githubusercontent.com/11669149/229570390-79a42021-17b4-4275-8def-4bf2eb783525.png">

6. Add data into an existing table __Student__ and verify
``` sql
insert into Student (ssn,firstname,lastname,birthDate)
values ('123456789','Amanda','Jones','1980-12-20')
;
```

```sql
select * from course;
```
<img width="852" alt="image" src="https://user-images.githubusercontent.com/11669149/229572297-4fa9e275-29a7-4e2a-9143-e34ec3bb8222.png">

7. Update data into an existing table __Student__ and verify
```sql
update student
set zipcode = '12345'
where ssn = '123456789';
```
```sql
 select * from student;
 ```
<img width="855" alt="image" src="https://user-images.githubusercontent.com/11669149/229572963-1af7c582-eb02-4381-b48a-4f4b816c7434.png">

8. Add another record in the table __Student__ and verify.


