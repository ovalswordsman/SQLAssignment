# SQLAssignment


## -- q1
create table employees(
	  EmpID int,
    Name varchar(20),
    Gender varchar(8),
	Department varchar(30)
);

insert into employees values 
	(1, "X", "Female" , "Finance"),
	(2, "Y", "Male" , "IT"),
	(3, "Z", "Male" , "HR"),
	(4, "W", "Female" , "IT");

SELECT department, 
       SUM(CASE WHEN gender = 'male' THEN 1 ELSE 0 END) AS Num_of_male, 
       SUM(CASE WHEN gender = 'female' THEN 1 ELSE 0 END) AS Num_of_female
FROM employees
GROUP BY department;

## -- q2
create table salary (
	Name varchar(20),
	Jan int,
	Feb int,
	Mar int
);

insert into salary values 

("X", 5200, 9093, 3832),
("Y", 9023, 8942, 4000),
("Z", 9834, 8197, 9903),
("W", 3244, 4321, 293);

SELECT Name,
GREATEST(Jan, Feb, Mar) AS Value,
ANY_VALUE(CASE
  WHEN Jan = GREATEST(Jan, Feb, Mar) THEN 'Jan'
  WHEN Feb = GREATEST(Jan, Feb, Mar) THEN 'Feb'
  WHEN Mar = GREATEST(Jan, Feb, Mar) THEN 'Mar'
  END) AS Month
FROM salary;

## -- q3
create table marks (
	Candidate_ID int, 
  Marks int
);

insert into marks values 
(1, 98),
(2, 78),
(3, 87),
(4, 98),
(5, 78);

SELECT Marks,
DENSE_RANK() OVER (ORDER BY Marks DESC) AS `Rank`,
GROUP_CONCAT(Candidate_ID ORDER BY Candidate_ID ASC) AS
Candidate_ID
FROM marks
GROUP BY Marks
ORDER BY `Rank`;

## -- q4
create table ID (
	candidate_ID int, 
  Email varchar(30)
);

insert into ID values
(45, "abc@gmail.com"),
(23, "def@yahoo.com"),
(34, "abc@gmail.com"),
(21, "bcf@gmail.com"),
(94, "def@yahoo.com");

DELETE c1
FROM ID c1
JOIN ID c2
ON c1.Email = c2.Email AND c1.Candidate_ID > c2.Candidate_ID;

select * from ID;
