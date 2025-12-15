# Employee_Mangement_System
A SQL-based Employee Management System that manages employees, job roles, departments, salaries, leaves, and payroll using normalized tables, foreign keys, joins, and aggregate queries.

# Employee Management System (SQL Project)

## 📌 Project Overview
The **Employee Management System (EMS)** is a SQL-based project designed to efficiently manage employee data within an organization.  
This system handles employee information, job roles, departments, qualifications, leave records, and payroll calculations using a normalized relational database.

# Employee Management System (SQL Project)

## 📌 Short Description (≈200 characters)
A SQL-based Employee Management System that manages employee details, job roles, departments, qualifications, leaves, and payroll using a normalized relational database and analytical queries.

---

## 📖 Project Overview
The **Employee Management System (EMS)** is a SQL project designed to efficiently manage employee-related data within an organization.  
It helps store, organize, and analyze employee details, job assignments, salaries, bonuses, leave records, qualifications, and payroll information.

This project demonstrates **real-world SQL usage**, making it ideal for:
- SQL interview preparation  
- Academic submissions  
- GitHub portfolio projects  

---

## 🛠️ Technologies Used
- SQL (MySQL / ANSI SQL)
- MySQL Workbench / Any SQL Editor

---

## 🗂️ Database Details
- **Database Name:** `employee`
- **Design:** Normalized (3NF)
- **Tables:** 6 interconnected tables
- **Data Integrity:** Enforced using Primary & Foreign Keys

---

## 🧱 Tables Included
| Table Name | Description |
|-----------|------------|
| JobDepartment | Stores job roles, departments, and salary ranges |
| SalaryBonus | Stores salary, bonus, and annual pay details |
| Employee | Stores employee personal and job details |
| Qualification | Tracks employee qualifications and skills |
| Leaves | Maintains employee leave records |
| Payroll | Calculates final payroll amounts |

---

## 🧾 Complete Table Creation SQL Code
```sql
-- Table 1: Job Department
CREATE TABLE JobDepartment (
    Job_ID INT PRIMARY KEY,
    jobdept VARCHAR(50),
    name VARCHAR(100),
    description TEXT,
    salaryrange VARCHAR(50)
);

-- Table 2: Salary and Bonus
CREATE TABLE SalaryBonus (
    salary_ID INT PRIMARY KEY,
    Job_ID INT,
    amount DECIMAL(10,2),
    annual DECIMAL(10,2),
    bonus DECIMAL(10,2),
    CONSTRAINT fk_salary_job FOREIGN KEY (Job_ID)
        REFERENCES JobDepartment(Job_ID)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- Table 3: Employee
CREATE TABLE Employee (
    emp_ID INT PRIMARY KEY,
    firstname VARCHAR(50),
    lastname VARCHAR(50),
    gender VARCHAR(10),
    age INT,
    contact_add VARCHAR(100),
    emp_email VARCHAR(100) UNIQUE,
    emp_pass VARCHAR(50),
    Job_ID INT,
    CONSTRAINT fk_employee_job FOREIGN KEY (Job_ID)
        REFERENCES JobDepartment(Job_ID)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);

-- Table 4: Qualification
CREATE TABLE Qualification (
    QualID INT PRIMARY KEY,
    Emp_ID INT,
    Position VARCHAR(50),
    Requirements VARCHAR(255),
    Date_In DATE,
    CONSTRAINT fk_qualification_emp FOREIGN KEY (Emp_ID)
        REFERENCES Employee(emp_ID)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- Table 5: Leaves
CREATE TABLE Leaves (
    leave_ID INT PRIMARY KEY,
    emp_ID INT,
    date DATE,
    reason TEXT,
    CONSTRAINT fk_leave_emp FOREIGN KEY (emp_ID)
        REFERENCES Employee(emp_ID)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- Table 6: Payroll
CREATE TABLE Payroll (
    payroll_ID INT PRIMARY KEY,
    emp_ID INT,
    job_ID INT,
    salary_ID INT,
    leave_ID INT,
    date DATE,
    report TEXT,
    total_amount DECIMAL(10,2),
    CONSTRAINT fk_payroll_emp FOREIGN KEY (emp_ID)
        REFERENCES Employee(emp_ID)
        ON DELETE CASCADE
        ON UPDATE CASCADE,
    CONSTRAINT fk_payroll_job FOREIGN KEY (job_ID)
        REFERENCES JobDepartment(Job_ID)
        ON DELETE CASCADE
        ON UPDATE CASCADE,
    CONSTRAINT fk_payroll_salary FOREIGN KEY (salary_ID)
        REFERENCES SalaryBonus(salary_ID)
        ON DELETE CASCADE
        ON UPDATE CASCADE,
    CONSTRAINT fk_payroll_leave FOREIGN KEY (leave_ID)
        REFERENCES Leaves(leave_ID)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);
```

## 🔗 Key Relationships

One Department → Many Employees

One Employee → Many Qualifications

One Employee → Many Leaves

Payroll links Employee, Job, Salary, and Leave data

## 🎯 Problem Statement

To design and implement a SQL-based Employee Management System that securely stores employee data, ensures data integrity using foreign keys, and enables payroll, leave tracking, and department-level analysis.

## 📊 Analysis Questions Covered
### Employee Insights

Total number of employees

Top 5 highest-paid employees

Average salary per department

Total salary expenditure

### Job & Department Analysis

Job roles per department

Highest-paying job roles

Department-wise salary allocation

### Qualification Analysis

Employees with qualifications

Roles requiring multiple qualifications

### Leave & Payroll Analysis

Employees with most leaves

Leave impact on payroll

Average payroll after deductions

## 🧠 SQL Concepts Used

DDL & DML

PRIMARY & FOREIGN KEYS

INNER JOIN

Aggregate Functions (SUM, AVG, COUNT)

CASCADE & SET NULL constraints


## ▶️ How to Run the Project

### Open MySQL Workbench

Create database:

CREATE DATABASE employee;
USE employee;


Run the SQL script

Verify using:

SHOW TABLES;


## 🗣️ Interview Explanation (Short)

“I designed a normalized SQL-based Employee Management System that handles employees, departments, salaries, leaves, and payroll using joins, constraints, and aggregate queries.”

### 📌 Learning Outcomes

Real-world database design

Payroll and HR data modeling

Advanced SQL joins and constraints


