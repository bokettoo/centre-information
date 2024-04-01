# Training Center Database

This repository contains the data modeling and tabular representation of persistent data for a training center. The data includes information about students and the training programs they are enrolled in.

## Overview

- Students choose the training program and its session in which they want to enroll and pay the training fee.
- Each student is identified by their National Identity Card (CIN) number. Upon registration, they are required to fill out an individual form containing their name, date of birth, address, city (Rabat, Casablanca, etc.), and educational level (Bac, Bac level, Bac+2, etc.).
- Then, from the training catalog, they must choose the desired program and the session related to that program. They also indicate the type of course they want to take (in-person or online). An enrollment form is kept by the administration.
- For each training program, the catalog specifies the code, title, duration, price, and specialties (code and name) related to that program, as well as the open sessions with their names, start date, and end date.
- Here are some management rules implemented by the center's management:
  - A student can be enrolled in multiple training sessions.
  - The training program can have multiple sessions.
  - A student cannot be enrolled in multiple sessions of the same training program.
  - A session is only opened if there are more than 10 enrolled students.
  - A training program can belong to multiple specialties.

## Tables

### Students Table

- Fields:
  - CIN (Primary Key)
  - Name
  - Date of Birth
  - Address
  - City
  - Educational Level

### Training Programs Table

- Fields:
  - Code (Primary Key)
  - Title
  - Duration
  - Price
  - Specialties (Code and Name)

### Sessions Table

- Fields:
  - Session ID (Primary Key)
  - Program Code (Foreign Key referencing Training Programs Table)
  - Session Name
  - Start Date
  - End Date

### Enrollments Table

- Fields:
  - Enrollment ID (Primary Key)
  - CIN (Foreign Key referencing Students Table)
  - Session ID (Foreign Key referencing Sessions Table)
  - Course Type (In-person or Online)
  - Enrollment Form

## Management Rules Implementation

1. A student can be enrolled in multiple sessions of different training programs.
2. A training program can have multiple sessions.
3. A student cannot be enrolled in multiple sessions of the same training program.
4. A session is only opened if there are more than 10 enrolled students.
5. A training program can belong to multiple specialties.

