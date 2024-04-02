
Below are some example SQL queries that can be used with the training center database:

1. Count the total number of students:
```sql
SELECT COUNT(*) FROM ETUDIANT;
```

2. Calculate the age of each student:
```sql
SELECT numCINetu, DATEDIFF(CURDATE(), datenaissance)/365.25 AS AGE FROM centremformation.etudiant;
```

3. Find the training program with the highest price:
```sql
SELECT codeForm, titreForm, MAX(prixForm) FROM centremformation.formation;
```

4. Find the training program with the lowest price:
```sql
SELECT codeForm, titreForm, MIN(prixForm) FROM centremformation.formation;
```

5. Calculate the total revenue generated from all training programs:
```sql
SELECT SUM(prixForm) FROM centremformation.formation;
```

6. Count the number of enrolled students for each session:
```sql
SELECT codeSess, COUNT(numCINetu) FROM centremformation.inscription GROUP BY codeSess;
```

7. Find the distinct CIN numbers of all enrolled students:
```sql
SELECT DISTINCT numCINetu FROM centremformation.inscription;
```

8. Count the number of sessions each student is enrolled in:
```sql
SELECT numCINetu, COUNT(codeSess) FROM centremformation.inscription GROUP BY numCINetu;
```

9. Count the number of enrollments for each session and course type:
```sql
SELECT codeSess, typeCours, COUNT(numinscription) FROM inscription GROUP BY codeSess, typeCours;
```
# Part 2

1. List sessions for each course
```sql
SELECT c.Title AS 'Course Title', s.Session_Name, s.Start_Date, s.End_Date
FROM Courses c
JOIN Sessions s ON c.Code = s.Course_Code;
```

 2. List enrolled students for each course
```sql
SELECT c.Title AS 'Course Title', s.Full_Name AS 'Student Name'
FROM Courses c
JOIN Enrollments e ON c.Code = e.Course_Code
JOIN Students s ON e.Student_CIN = s.CIN
ORDER BY c.Title;
```

3. Calculate online and in-person enrollments for web development course
```sql
SELECT
    SUM(CASE WHEN e.Course_Type = 'Online' THEN 1 ELSE 0 END) AS 'Online Enrollments',
    SUM(CASE WHEN e.Course_Type = 'In-person' THEN 1 ELSE 0 END) AS 'In-person Enrollments'
FROM Courses c
JOIN Enrollments e ON c.Code = e.Course_Code
WHERE c.Title = 'Web Development';
```

4. List courses with 3 or more online enrollments
```sql
SELECT c.Title, COUNT(*) AS 'Online Enrollments'
FROM Courses c
JOIN Enrollments e ON c.Code = e.Course_Code
WHERE e.Course_Type = 'Online'
GROUP BY c.Title
HAVING COUNT(*) >= 3
ORDER BY COUNT(*) DESC;
```

5. List active specialties with corresponding courses
```sql
SELECT s.Specialty_Name, c.Title, c.Duration, c.Price
FROM Courses c
JOIN Specialties_Courses sc ON c.Code = sc.Course_Code
JOIN Specialties s ON sc.Specialty_Code = s.Specialty_Code
ORDER BY s.Specialty_Name DESC, c.Title;
```

6. Union of courses with 4 or more in-person enrollments and courses with 4 or more online enrollments
```sql
(
    SELECT c.Title, COUNT(*) AS 'In-person Enrollments'
    FROM Courses c
    JOIN Enrollments e ON c.Code = e.Course_Code
    WHERE e.Course_Type = 'In-person'
    GROUP BY c.Title
    HAVING COUNT(*) >= 4
)
UNION
(
    SELECT c.Title, COUNT(*) AS 'Online Enrollments'
    FROM Courses c
    JOIN Enrollments e ON c.Code = e.Course_Code
    WHERE e.Course_Type = 'Online'
    GROUP BY c.Title
    HAVING COUNT(*) >= 4
);
```

7. Calculate total fees paid per year and month of session start date
```sql
SELECT YEAR(s.Start_Date) AS 'Year', MONTH(s.Start_Date) AS 'Month', SUM(c.Price) AS 'Total Fees'
FROM Sessions s
JOIN Courses c ON s.Course_Code = c.Code
GROUP BY YEAR(s.Start_Date), MONTH(s.Start_Date)
ORDER BY YEAR(s.Start_Date), MONTH(s.Start_Date);
```

These MySQL queries address the specified questions for the given exercise. Each query is designed to retrieve the required information from the database schema provided.
