# my-first-SQL-projects
"This is my first project on GitHub."

-- ==============================
-- Employee Management System
-- Database: EmployeeManagement
-- ==============================

-- Drop tables if they exist
DROP TABLE IF EXISTS EmployeeProjects;
DROP TABLE IF EXISTS Employees;
DROP TABLE IF EXISTS Projects;
DROP TABLE IF EXISTS Departments;

-- Create Departments table
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(50) NOT NULL
);

-- Create Employees table
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL,
    DepartmentID INT,
    DateOfJoining DATE,
    Salary DECIMAL(10,2),
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);

-- Create Projects table
CREATE TABLE Projects (
    ProjectID INT PRIMARY KEY,
    ProjectName VARCHAR(100) NOT NULL,
    StartDate DATE,
    EndDate DATE
);

-- Create EmployeeProjects table (Many-to-Many)
CREATE TABLE EmployeeProjects (
    EmployeeID INT,
    ProjectID INT,
    AssignedDate DATE,
    PRIMARY KEY (EmployeeID, ProjectID),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
    FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);

-- ==============================
-- Insert Sample Data
-- ==============================

-- Departments
INSERT INTO Departments VALUES 
(1, 'HR'), 
(2, 'IT'), 
(3, 'Finance');

-- Employees
INSERT INTO Employees VALUES
(101, 'Alice', 'Smith', 'alice@example.com', 2, '2023-01-15', 5000),
(102, 'Bob', 'Brown', 'bob@example.com', 2, '2022-06-01', 4500),
(103, 'Charlie', 'Davis', 'charlie@example.com', 1, '2021-09-20', 4000),
(104, 'Diana', 'Clark', 'diana@example.com', 3, '2020-03-15', 4800);

-- Projects
INSERT INTO Projects VALUES
(201, 'Website Redesign', '2023-01-01', '2023-06-30'),
(202, 'Payroll System', '2023-02-01', '2023-12-31');

-- EmployeeProjects
INSERT INTO EmployeeProjects VALUES
(101, 201, '2023-01-10'),
(102, 201, '2023-01-12'),
(103, 202, '2023-02-05'),
(104, 202, '2023-02-10');
-- ==============================
-- Showcase Queries
-- ==============================

-- 1️⃣ Simple SELECT
SELECT * FROM Employees;

-- 2️⃣ Join Tables
-- Show Employee with Department Name
SELECT e.FirstName, e.LastName, d.DepartmentName
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DepartmentID;

-- 3️⃣ Aggregation
-- Average salary per department
SELECT d.DepartmentName, AVG(e.Salary) AS AvgSalary
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DepartmentID
GROUP BY d.DepartmentName;

-- 4️⃣ Subquery
-- Employees earning more than average salary
SELECT FirstName, LastName, Salary
FROM Employees
WHERE Salary > (SELECT AVG(Salary) FROM Employees);

-- 5️⃣ Insert / Update / Delete
-- Add new employee
INSERT INTO Employees VALUES (105, 'Evan', 'Lee', 'evan@example.com', 2, '2023-11-01', 4700);

-- Update salary
UPDATE Employees SET Salary = 5200 WHERE EmployeeID = 101;

-- Delete an employee
DELETE FROM Employees WHERE EmployeeID = 105;

-- 6️⃣ Complex Query with Many-to-Many
-- List employees and their projects
SELECT e.FirstName, e.LastName, p.ProjectName
FROM Employees e
JOIN EmployeeProjects ep ON e.EmployeeID = ep.EmployeeID
JOIN Projects p ON ep.ProjectID = p.ProjectID;
# Employee Management System

A simple SQL project demonstrating:

- Table creation with relationships
- CRUD operations (Create, Read, Update, Delete)
- Joins, Aggregation, and Subqueries
- Many-to-Many relationships

## Database Schema

- Departments
- Employees
- Projects
- EmployeeProjects

## How to Run

1. Run `schema.sql` to create tables.
2. Run `sample_data.sql` to insert sample data.
3. Run `queries.sql` to see example queries.

## Project Structure


