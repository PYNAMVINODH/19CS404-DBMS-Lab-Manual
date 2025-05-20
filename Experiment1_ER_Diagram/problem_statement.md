# Experiment 1: Entity-Relationship (ER) Diagram

## 🎯 Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.

## 📚 Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.

---

## 🧪 Choose One Scenario:

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

## 📝 Tasks:
1. Identify entities, relationships, and attributes.
2. Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).
3. Include:
   - Cardinality & participation constraints
   - Prerequisites for University OR Billing for Hospital
4. Explain:
   - Why you chose the entities and relationships.
   - How you modeled prerequisites or billing.

# ER Diagram Submission - PYNAM VINODH

## Scenario Chosen:
University / Hospital (choose one)

## ER Diagram:
![image](https://github.com/user-attachments/assets/20b4bc30-c8e5-49a0-b2ce-a09e6e770899)


## Entities and Attributes:
PATIENT
Attributes: Patient_ID (PK), Name, Gender, DOB, PhoneNumber

DOCTOR
Attributes: Doctor_ID (PK), Name, Specialization, PhoneNumber

DEPARTMENT
Attributes: Department_ID (PK), Department_Name, Department_Head

MEDICAL_RECORD
Attributes: MedicalRecord_ID (PK), Patient_Medical_Details, Medicines_Prescribed

APPOINTMENT
Attributes: Appointment_ID (PK), Cause_Of_Visit, Appointment_Date_And_Time

PAYMENTS
Attributes: Payment_ID (PK), Date_Of_Payment, Amount
...

## Relationships and Constraints:
CONSULTS (Between PATIENT and DOCTOR)
Cardinality: M:N

MANAGES (Between DOCTOR and DEPARTMENT)
Cardinality: M:1

HANDLES (Between DEPARTMENT and PAYMENTS)
Cardinality: 1:N

PATIENT PERSONAL DATA (Between PATIENT and MEDICAL_RECORD)
Cardinality: 1:N

DELIVERED FORM (Between MEDICAL_RECORD and APPOINTMENT)
Cardinality: 1:N

COST OF CONSULTATION (Between APPOINTMENT and PAYMENTS)
Cardinality: 1:1
...

## Extension (Prerequisite / Billing):
COST OF CONSULTATION (APPOINTMENT–PAYMENTS)
Attributes: Not explicitly listed beyond those in PAYMENTS entity
Cardinality: 1:1

## Design Choices:
Surrogate Keys like Patient_ID, Doctor_ID, Department_ID, etc., are used as unique identifiers.

M:N relationships like CONSULTS are clearly modeled.

Relationship "DELIVERED FORM" connects appointments and medical records, ensuring traceability.

Normalization is evident with separate entities for medical records, payments, appointments, etc.

## RESULT
Tables:

PATIENT (Patient_ID, Name, Gender, DOB, PhoneNumber)
DOCTOR (Doctor_ID, Name, Specialization, PhoneNumber)
DEPARTMENT (Department_ID, Department_Name, Department_Head)
MEDICAL_RECORD (MedicalRecord_ID, Patient_Medical_Details, Medicines_Prescribed)
APPOINTMENT (Appointment_ID, Cause_Of_Visit, Appointment_Date_And_Time)
PAYMENTS (Payment_ID, Date_Of_Payment, Amount)

Associative (Relation) Tables:

CONSULTS (Patient_ID, Doctor_ID)
MANAGES (Doctor_ID, Department_ID)
HANDLES (Department_ID, Payment_ID)
PATIENT_PERSONAL_DATA (Patient_ID, MedicalRecord_ID)
DELIVERED_FORM (MedicalRecord_ID, Appointment_ID)
COST_OF_CONSULTATION (Appointment_ID, Payment_ID)
