
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
