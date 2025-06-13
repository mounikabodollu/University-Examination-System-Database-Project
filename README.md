# 📚 University Course Management System

A relational database project to manage departments, courses, faculty, students, enrollments, and assignments in a university setting.

---

## 🧾 Project Overview

This database models an academic system with the following entities:

| Entity      | Description                                                  |
|-------------|--------------------------------------------------------------|
| **Department** | Departments within the university (e.g., CS, Electronics)     |
| **Course**     | Courses offered by departments (e.g., DBMS, Networks)         |
| **Faculty**    | Faculty members who teach or coordinate courses              |
| **Student**    | Students who enroll in and attend courses                    |
| **EnrollsIn**  | Join table tracking student enrollments and attendance       |
| **TaughtBy**   | Join table linking faculty to the courses they teach         |
| **CoordinatedBy** | Mapping of each course to its assigned coordinator       |

---

## ⚙️ Features

- **One-to-many**: Departments to courses, faculty, and students.
- **Many-to-many** with attributes:
  - Students enroll in multiple courses – attendance tracked.
- **Many-to-many**:
  - Faculty teaching multiple courses.
- **One-to-one** (optional constraint): Each course has one coordinator.

---

## 📂 Database Schema & Sample Data

```sql
-- Department
CREATE TABLE Department (
  DeptID INT PRIMARY KEY,
  DeptName VARCHAR(100)
);
INSERT INTO Department VALUES (1, 'Computer Science'), (2, 'Electronics');

-- Course
CREATE TABLE Course (
  CourseID INT PRIMARY KEY,
  CourseName VARCHAR(100),
  DeptID INT REFERENCES Department(DeptID)
);
INSERT INTO Course VALUES (101, 'DBMS', 1), (102, 'Networks', 2);

-- Faculty
CREATE TABLE Faculty (
  FacultyID INT PRIMARY KEY,
  FacultyName VARCHAR(100),
  DeptID INT REFERENCES Department(DeptID)
);
INSERT INTO Faculty VALUES (201, 'Dr. A Kumar', 1), (202, 'Dr. B Rao', 2);

-- Student
CREATE TABLE Student (
  StudentID INT PRIMARY KEY,
  StudentName VARCHAR(100),
  DeptID INT REFERENCES Department(DeptID)
);
INSERT INTO Student VALUES (301, 'Meena', 1), (302, 'Ravi', 2);

-- EnrollsIn (Student–Course with attendance)
CREATE TABLE EnrollsIn (
  StudentID INT REFERENCES Student(StudentID),
  CourseID INT REFERENCES Course(CourseID),
  Attendance INT,
  PRIMARY KEY (StudentID, CourseID)
);
INSERT INTO EnrollsIn VALUES (301, 101, 90), (302, 102, 85);

-- TaughtBy (Faculty teaches Course)
CREATE TABLE TaughtBy (
  CourseID INT REFERENCES Course(CourseID),
  FacultyID INT REFERENCES Faculty(FacultyID),
  PRIMARY KEY (CourseID, FacultyID)
);
INSERT INTO TaughtBy VALUES (101, 201), (102, 202);

-- CoordinatedBy (Single faculty coordinator per course)
CREATE TABLE CoordinatedBy (
  CourseID INT PRIMARY KEY REFERENCES Course(CourseID),
  FacultyID INT REFERENCES Faculty(FacultyID)
);
INSERT INTO CoordinatedBy VALUES (101, 201), (102, 202);

![image](https://github.com/user-attachments/assets/6cc825e9-86c4-41b8-9c71-cd4320373d71)

![image](https://github.com/user-attachments/assets/f9a2ff19-1986-4958-8a6e-40b69383e964)

