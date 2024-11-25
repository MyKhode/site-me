---
title: Student Management System (MIS) with Java, IntelliJ, and LGoodDatePicker
published: 2024-03-24
description: 'A comprehensive guide to building a Student Management Information System (MIS) using Java with IntelliJ IDE. This project showcases how to manage student data using MySQL, with a focus on CRUD operations and GUI development using Java Swing.'
image: 'https://github.com/user-attachments/assets/57aac562-8651-4e5d-9914-e93bec96e82d'
tags: [ 
    "Java",
    "Programming",
    "School Project",
    "Year 2",
    "IntelliJ",
    "MySQL",
    "Student Management"
]
category: 'App'
draft: false 
---
<div align="center">

# 🏅 Student Management Information System (MIS) with Java and IntelliJ 🏅
<img alt="GitHub License" src="https://img.shields.io/github/license/ikhode-arena/MIS-Java-Intellij">
<img alt="GitHub forks" src="https://img.shields.io/github/forks/ikhode-arena/MIS-Java-Intellij">
<img alt="GitHub Release" src="https://img.shields.io/github/v/release/ikhode-arena/mis-java-intellij">
<img alt="GitHub code size in bytes" src="https://img.shields.io/github/languages/code-size/ikhode-arena/MIS-Java-Intellij">

</div>

## 🎯 Project Overview

This project focuses on developing a Student Management Information System (MIS) using Java with the IntelliJ IDE. The system uses a MySQL database to handle CRUD operations (Create, Read, Update, Delete) for managing student data. It also features a user-friendly GUI developed using Java Swing.

### Key Features

- **Java Swing GUI**: A graphical user interface designed using Java Swing within IntelliJ.
- **MySQL Integration**: Connects to a MySQL database to handle student data.
- **LGoodDatePicker Integration**: Implements LGoodDatePicker to enhance date selection in the GUI.
- **CRUD Operations**: Enables users to perform Create, Read, Update, and Delete operations on student records.
- **Error Handling**: Implements error handling with try-catch blocks to ensure smooth operation.

## 💪 Installation Guide

Follow these steps to set up and run the project:

1. **Download MySQL Connector/J**:
   - Ensure that you have the MySQL Connector/J library for Java.
2. **Download LGoodDatePicker**:
   - Include the LGoodDatePicker library in your project dependencies for advanced date handling.

3. **Import into IntelliJ**:
   - Import the project into IntelliJ by setting up the project structure and adding necessary dependencies.

4. **MySQL Database Setup**:
   - Import the provided MySQL database script into your MySQL server.

5. **Run the Project**:
   - Execute the project via the IntelliJ GUI.

## 🏹 MySQL Scripting

The following script creates the necessary database and tables for the Student Management Information System:

```sql
-- phpMyAdmin SQL Dump
-- version 5.2.1
-- https://www.phpmyadmin.net/
--
-- Host: 127.0.0.1
-- Generation Time: Aug 02, 2024 at 12:45 PM
-- Server version: 10.4.32-MariaDB
-- PHP Version: 8.2.12

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+00:00";

-- Database: `java_activity_1`

-- Table structure for table `gender`
CREATE TABLE `gender` (
  `id` int(11) NOT NULL,
  `gender_name` varchar(50) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- Insert data into `gender`
INSERT INTO `gender` (`id`, `gender_name`) VALUES
(1, 'Male'),
(2, 'Female'),
(3, 'Other');

-- Table structure for table `student`
CREATE TABLE `student` (
  `id` int(11) NOT NULL,
  `name_latin` varchar(200) NOT NULL,
  `name_khmer` varchar(200) NOT NULL,
  `gender_id` int(11) NOT NULL,
  `date_of_birth` date NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- Insert data into `student`
INSERT INTO `student` (`id`, `name_latin`, `name_khmer`, `gender_id`, `date_of_birth`) VALUES
(2, 'Jane Smith', 'ជាន ស្មិច', 2, '2001-02-20'),
(3, 'Alex Kim', 'អាលិច គីម', 3, '1999-05-30'),
(4, 'Test User', 'តេស', 1, '2024-08-08');

-- Indexes and constraints
ALTER TABLE `gender`
  ADD PRIMARY KEY (`id`);

ALTER TABLE `student`
  ADD PRIMARY KEY (`id`),
  ADD KEY `gender_id` (`gender_id`);

ALTER TABLE `gender`
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=4;

ALTER TABLE `student`
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=5;

ALTER TABLE `student`
  ADD CONSTRAINT `student_ibfk_1` FOREIGN KEY (`gender_id`) REFERENCES `gender` (`id`);

COMMIT;
```

## 🔯 Demo

![image](https://github.com/user-attachments/assets/57aac562-8651-4e5d-9914-e93bec96e82d)


### ✍️ Citation

```bibtex
@misc{java_intellij_mis,
  author = {SOY TET},
  title = {Student Management Information System (MIS) with Java and IntelliJ},
  year = {2024},
  publisher = {GitHub},
  journal = {GitHub repository}
}

```

---
### 👨‍🎓 References
- [Java Swing Documentation](https://docs.oracle.com/javase/tutorial/uiswing/)
- [MySQL Connector/J Documentation](https://dev.mysql.com/downloads/connector/j/)
- [IntelliJ IDEA Documentation](https://www.jetbrains.com/idea/resources/)
- [LGoodDatePicker Date Time Select Library](https://github.com/LGoodDatePicker/LGoodDatePicker)
---
