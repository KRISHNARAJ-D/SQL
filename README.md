# SQL
# Student Management System – SQL Schema

This project uses **MySQL** as the database to store and manage student, course, and enrollment details.

## Database Structure
1. **students** – Stores student personal and contact information.
2. **courses** – Stores course name, duration, and fee details.
3. **enrollments** – Acts as a link between students and courses (Many-to-Many relationship).

## Features
- Auto-incremented primary keys for unique identification.
- `FOREIGN KEY` constraints to maintain referential integrity.
- Cascading deletes to ensure data consistency.
- Sample data insertion for quick testing.

## SQL-CODE
```
-- Create Database
CREATE DATABASE student_management;

-- Use the database
USE student_management;

-- Create table for storing student details
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    dob DATE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    phone VARCHAR(15),
    enrollment_date DATE DEFAULT CURRENT_DATE
);

-- Create table for storing course details
CREATE TABLE courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    duration_months INT NOT NULL,
    fee DECIMAL(10, 2) NOT NULL
);

-- Create table for enrollments (Many-to-Many relationship)
CREATE TABLE enrollments (
    enrollment_id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT NOT NULL,
    course_id INT NOT NULL,
    enrollment_date DATE DEFAULT CURRENT_DATE,
    FOREIGN KEY (student_id) REFERENCES students(student_id) ON DELETE CASCADE,
    FOREIGN KEY (course_id) REFERENCES courses(course_id) ON DELETE CASCADE
);

-- Insert sample student data
INSERT INTO students (first_name, last_name, dob, email, phone) VALUES
('John', 'Doe', '2000-05-15', 'john.doe@example.com', '9876543210'),
('Jane', 'Smith', '1999-08-20', 'jane.smith@example.com', '9876501234');

-- Insert sample courses
INSERT INTO courses (course_name, duration_months, fee) VALUES
('Java Programming', 6, 12000.00),
('Database Management', 4, 8000.00);
```
