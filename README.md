1. Course name and total number of students in each course
SELECT course, COUNT(*) AS total_students
FROM Students
GROUP BY course;

Expected Output:

course	total_students
SQL	4
Java	3
Python	3
2. Course name and average marks where average marks > 75
SELECT course, AVG(marks) AS average_marks
FROM Students
GROUP BY course
HAVING AVG(marks) > 75;

Expected Output:

course	average_marks
Java	81.67
Python	78.33
SQL	75.00

Result: Java and Python only, because SQL's average is exactly 75, not greater than 75.

3. Total marks in each city, descending order
SELECT city, SUM(marks) AS total_marks
FROM Students
GROUP BY city
ORDER BY total_marks DESC;

Expected Output:

city	total_marks
Hyderabad	421
Chennai	304
Bangalore	248
4. Course, highest marks, and lowest marks
SELECT course,
       MAX(marks) AS highest_marks,
       MIN(marks) AS lowest_marks
FROM Students
GROUP BY course;

Expected Output:

course	highest_marks	lowest_marks
SQL	90	55
Java	95	72
Python	88	65
5. Cities having more than 2 students
SELECT city, COUNT(*) AS total_students
FROM Students
GROUP BY city
HAVING COUNT(*) > 2;

Expected Output:

city	total_students
Hyderabad	5
Chennai	3
6. Average age in each course where average age > 21
SELECT course, AVG(age) AS average_age
FROM Students
GROUP BY course
HAVING AVG(age) > 21;

Expected Output:

course	average_age
SQL	23.50
Java	22.00
Python	21.67
7. Course and total marks where total marks > 200
SELECT course, SUM(marks) AS total_marks
FROM Students
GROUP BY course
HAVING SUM(marks) > 200;

Expected Output:

course	total_marks
SQL	300
Java	245
Python	235
8. City, maximum and minimum marks, ordered by maximum marks descending
SELECT city,
       MAX(marks) AS maximum_marks,
       MIN(marks) AS minimum_marks
FROM Students
GROUP BY city
ORDER BY maximum_marks DESC;

Expected Output:

city	maximum_marks	minimum_marks
Bangalore	95	65
Hyderabad	90	70
Chennai	82	55
9. Courses having at least 3 students
SELECT course, COUNT(*) AS total_students
FROM Students
GROUP BY course
HAVING COUNT(*) >= 3;

Expected Output:

course	total_students
SQL	4
Java	3
Python	3
10. Course average marks and total marks where average is between 70 and 90
SELECT course,
       AVG(marks) AS average_marks,
       SUM(marks) AS total_marks
FROM Students
GROUP BY course
HAVING AVG(marks) BETWEEN 70 AND 90;

Expected Output:

course	average_marks	total_marks
SQL	75.00	300
Java	81.67	245
Python	78.33	235
11. City, number of students, and average marks

Conditions:

More than 2 students
Average marks > 75
Average marks descending
SELECT city,
       COUNT(*) AS total_students,
       AVG(marks) AS average_marks
FROM Students
GROUP BY city
HAVING COUNT(*) > 2
   AND AVG(marks) > 75
ORDER BY average_marks DESC;

Expected Output:

city	total_students	average_marks
Hyderabad	5	84.20
12. Course details where students > 2 and highest marks > 85
SELECT course,
       COUNT(*) AS total_students,
       MAX(marks) AS highest_marks,
       MIN(marks) AS lowest_marks,
       AVG(marks) AS average_marks
FROM Students
GROUP BY course
HAVING COUNT(*) > 2
   AND MAX(marks) > 85
ORDER BY average_marks DESC;

Expected Output:

course	total_students	highest_marks	lowest_marks	average_marks
Java	3	95	72	81.67
Python	3	88	65	78.33
SQL	4	90	55	75.00
13. Total marks for each course in each city > 150
SELECT course,
       city,
       SUM(marks) AS total_marks
FROM Students
GROUP BY course, city
HAVING SUM(marks) > 150;

Expected Output:

course	city	total_marks
SQL	Hyderabad	245
14. Course and city with student count, total marks, average marks
SELECT course,
       city,
       COUNT(*) AS total_students,
       SUM(marks) AS total_marks,
       AVG(marks) AS average_marks
FROM Students
GROUP BY course, city
HAVING COUNT(*) > 1
ORDER BY total_marks DESC;

Expected Output:

course	city	total_students	total_marks	average_marks
SQL	Hyderabad	3	245	81.67
Java	Hyderabad	1	78	78.00
Python	Chennai	1	82	82.00
SQL	Chennai	1	55	55.00
Python	Hyderabad	1	88	88.00
Java	Bangalore	1	95	95.00
SQL	Hyderabad?	—	—	—

⚠️ Correction: Because GROUP BY course, city requires the combination to have more than 1 student, the actual output is:

course	city	total_students	total_marks	average_marks
SQL	Hyderabad	3	245	81.67

There are no other course-city combinations with more than one student.

15. City-wise highest marks where average marks > 75
SELECT city,
       MAX(marks) AS highest_marks
FROM Students
GROUP BY city
HAVING AVG(marks) > 75;

Expected Output:

city	highest_marks
Hyderabad	90
16. Course-wise average marks for students whose marks > 60

Show only courses where average > 80.

SELECT course,
       AVG(marks) AS average_marks
FROM Students
WHERE marks > 60
GROUP BY course
HAVING AVG(marks) > 80;

Expected Output:

course	average_marks
Java	81.67
17. Course total marks for Hyderabad or Chennai
SELECT course,
       SUM(marks) AS total_marks
FROM Students
WHERE city IN ('Hyderabad', 'Chennai')
GROUP BY course
HAVING SUM(marks) > 150
ORDER BY total_marks DESC;

Expected Output:

course	total_marks
SQL	300
Java	150
Python	170

⚠️ Since the condition is SUM(marks) > 150, Java is excluded because its total is exactly 150.

Therefore the correct output is:

course	total_marks
SQL	300
Python	170
18. City, course, number of students and average marks

Conditions:

Age > 21
More than 1 student per group
Average marks > 70
SELECT city,
       course,
       COUNT(*) AS total_students,
       AVG(marks) AS average_marks
FROM Students
WHERE age > 21
GROUP BY city, course
HAVING COUNT(*) > 1
   AND AVG(marks) > 70;

Expected Output:

city	course	total_students	average_marks
Hyderabad	SQL	3	81.67
19. Highest and lowest marks for each course — Hyderabad only

Difference between highest and lowest must be > 10.

SELECT course,
       MAX(marks) AS highest_marks,
       MIN(marks) AS lowest_marks
FROM Students
WHERE city = 'Hyderabad'
GROUP BY course
HAVING MAX(marks) - MIN(marks) > 10;

Expected Output:

course	highest_marks	lowest_marks
SQL	90	70
20. Final Challenge

Conditions:

Marks >= 60
Group by city and course
More than 1 student
Average marks > 75
Average marks descending
Total students descending
SELECT city,
       course,
       COUNT(*) AS total_students,
       SUM(marks) AS total_marks,
       AVG(marks) AS average_marks,
       MAX(marks) AS highest_marks,
       MIN(marks) AS lowest_marks
FROM Students
WHERE marks >= 60
GROUP BY city, course
HAVING COUNT(*) > 1
   AND AVG(marks) > 75
ORDER BY average_marks DESC,
         total_students DESC;

Expected Output:

city	course	total_students	total_marks	average_marks	highest_marks	lowest_marks
Hyderabad	SQL	3	245	81.67	90	70
⚠️ Important correction for Query 14

The correct Query 14 is simply:

SELECT course,
       city,
       COUNT(*) AS total_students,
       SUM(marks) AS total_marks,
       AVG(marks) AS average_marks
FROM Students
GROUP BY course, city
HAVING COUNT(*) > 1
ORDER BY total_marks DESC;

Only SQL + Hyderabad has more than one student, so only that row appears.

Complete submission order

For your re-upload, use these 20 queries exactly in order:

-- 1
SELECT course, COUNT(*) AS total_students
FROM Students
GROUP BY course;

-- 2
SELECT course, AVG(marks) AS average_marks
FROM Students
GROUP BY course
HAVING AVG(marks) > 75;

-- 3
SELECT city, SUM(marks) AS total_marks
FROM Students
GROUP BY city
ORDER BY total_marks DESC;

-- 4
SELECT course, MAX(marks) AS highest_marks, MIN(marks) AS lowest_marks
FROM Students
GROUP BY course;

-- 5
SELECT city, COUNT(*) AS total_students
FROM Students
GROUP BY city
HAVING COUNT(*) > 2;

-- 6
SELECT course, AVG(age) AS average_age
FROM Students
GROUP BY course
HAVING AVG(age) > 21;

-- 7
SELECT course, SUM(marks) AS total_marks
FROM Students
GROUP BY course
HAVING SUM(marks) > 200;

-- 8
SELECT city, MAX(marks) AS maximum_marks, MIN(marks) AS minimum_marks
FROM Students
GROUP BY city
ORDER BY maximum_marks DESC;

-- 9
SELECT course, COUNT(*) AS total_students
FROM Students
GROUP BY course
HAVING COUNT(*) >= 3;

-- 10
SELECT course, AVG(marks) AS average_marks, SUM(marks) AS total_marks
FROM Students
GROUP BY course
HAVING AVG(marks) BETWEEN 70 AND 90;

-- 11
SELECT city, COUNT(*) AS total_students, AVG(marks) AS average_marks
FROM Students
GROUP BY city
HAVING COUNT(*) > 2
   AND AVG(marks) > 75
ORDER BY average_marks DESC;

-- 12
SELECT course,
       COUNT(*) AS total_students,
       MAX(marks) AS highest_marks,
       MIN(marks) AS lowest_marks,
       AVG(marks) AS average_marks
FROM Students
GROUP BY course
HAVING COUNT(*) > 2
   AND MAX(marks) > 85
ORDER BY average_marks DESC;

-- 13
SELECT course, city, SUM(marks) AS total_marks
FROM Students
GROUP BY course, city
HAVING SUM(marks) > 150;

-- 14
SELECT course, city,
       COUNT(*) AS total_students,
       SUM(marks) AS total_marks,
       AVG(marks) AS average_marks
FROM Students
GROUP BY course, city
HAVING COUNT(*) > 1
ORDER BY total_marks DESC;

-- 15
SELECT city, MAX(marks) AS highest_marks
FROM Students
GROUP BY city
HAVING AVG(marks) > 75;

-- 16
SELECT course, AVG(marks) AS average_marks
FROM Students
WHERE marks > 60
GROUP BY course
HAVING AVG(marks) > 80;

-- 17
SELECT course, SUM(marks) AS total_marks
FROM Students
WHERE city IN ('Hyderabad', 'Chennai')
GROUP BY course
HAVING SUM(marks) > 150
ORDER BY total_marks DESC;

-- 18
SELECT city, course,
       COUNT(*) AS total_students,
       AVG(marks) AS average_marks
FROM Students
WHERE age > 21
GROUP BY city, course
HAVING COUNT(*) > 1
   AND AVG(marks) > 70;

-- 19
SELECT course,
       MAX(marks) AS highest_marks,
       MIN(marks) AS lowest_marks
FROM Students
WHERE city = 'Hyderabad'
GROUP BY course
HAVING MAX(marks) - MIN(marks) > 10;

-- 20
SELECT city,
       course,
       COUNT(*) AS total_students,
       SUM(marks) AS total_marks,
       AVG(marks) AS average_marks,
       MAX(marks) AS highest_marks,
       MIN(marks) AS lowest_marks
FROM Students
WHERE marks >= 60
GROUP BY city, course
HAVING COUNT(*) > 1
   AND AVG(marks) > 75
ORDER BY average_marks DESC,
         total_students DESC;
