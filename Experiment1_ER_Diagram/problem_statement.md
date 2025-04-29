# Experiment 1: Entity-Relationship (ER) Diagram

## 🎯 Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.

## 📚 Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.

---

### 🔹 Scenario 1: University Database
Design a database to manage students, instructors, programs, courses, and student enrollments. Include prerequisites for courses.

**User Requirements:**
- Academic programs grouped under departments.
- Students have admission number, name, DOB, contact info.
- Instructors with staff number, contact info, etc.
- Courses have number, name, credits.
- Track course enrollments by students and enrollment date.
- Add support for prerequisites (some courses require others).

---

### 🔹 Scenario 2: Hospital Database
Design a database for patient management, appointments, medical records, and billing.

**User Requirements:**
- Patient details including contact and insurance.
- Doctors and their departments, contact info, specialization.
- Appointments with reason, time, patient-doctor link.
- Medical records with treatments, diagnosis, test results.
- Billing and payment details for each appointment.

---

# ER Diagram Submission - JOHN CHRISTOBER T

## Scenario Chosen:
University

## ER Diagram:
![image](https://github.com/user-attachments/assets/b1b50efd-750e-40fa-8289-7f02a1d39254)


## Entities and Attributes:
Student
Attributes: Register No (Primary Key), Name, Subjects Enrolled, Mobile No, Mail ID

Department
Attributes: Dept ID (Primary Key), Dept Name

Programs
Attributes: Program Code (Primary Key), Program Name, Subjects

University
Attributes: University ID (Primary Key), University Name, Students and Faculties

Instructors
Attributes: Instructor ID (Primary Key), Name, Subject

Courses
Attributes: Course Code (Primary Key), Course Name, Credits, Instructor Handling

## Relationships and Constraints:
In a (Between Student and Department)
Cardinality: M:N
Participation: Total (implied for both)

Provides (Between Department and Programs)
Cardinality: M:N
Participation: Partial

Contains (Between Programs and Courses)
Cardinality: M:N
Participation: Total for Courses (implied)

Enrolls in (Between Student and Courses)
Cardinality: M:N
Participation: Total for Students (every student must enroll in at least one course)

Teaches (Between Instructors and Courses)
Cardinality: 1:N
Participation: Total for Instructors, Partial for Courses

Has (Between University and Student, and University and Instructors)
Cardinality: 1:N
Participation: Total for Students and Instructors

## Design Choices:
Normalization: Each logical entity has its own table (e.g., Student, Instructor, Courses), reducing redundancy.

Modular design: Department acts as a bridge between students and programs, reflecting real academic structures.

M:N Relationships: Used to allow flexibility—e.g., students enrolled in multiple departments or courses.

Scalability: Supports future expansions like new departments, courses, or programs.

## RESULT
A complete ER model of a university system that defines students, courses, professors, and their interrelationships, including prerequisites, with proper constraints and rationale.
