# Transactions in Java JDBC Exercises



## Exercise 1: Implement a transaction to transfer funds from one account to another

Develop a Java program that can transfer funds from one account to another within a transaction. The program should handle errors and rollback the transaction if any error occurs during the fund transfer process. The program should perform the following steps:

1. Establish a connection to the database.
2. Disable auto-commit mode to start a transaction.
3. Update the balance of the source account by subtracting the transfer amount.
4. Update the balance of the destination account by adding the transfer amount.
5. Commit the transaction if both updates are successful.
6. If any error occurs during the transaction, roll back the transaction.

## Exercise 2: Implement a transaction to insert data into multiple tables

Write a Java program that can insert data into multiple related tables within a single transaction. The program should ensure data consistency and integrity across all tables involved in the transaction. The program should perform the following steps:

1. Establish a connection to the database.
2. Disable auto-commit mode to start a transaction.
3. Insert a new student record into the "students" table.
4. Insert a new course record into the "courses" table.
5. Insert a new enrollment record into the "enrollments" table, linking the student and course.
6. Commit the transaction if all insertions are successful.
7. If any error occurs during the transaction, roll back the transaction.

## Exercise 3: Implement a transaction to update data across multiple tables

Develop a Java program that can update data across multiple related tables within a single transaction. The program should handle errors and rollback the transaction if any error occurs during the update process. The program should perform the following steps:

1. Establish a connection to the database.
2. Disable auto-commit mode to start a transaction.
3. Update the age of a student in the "students" table.
4. Update the credits of a course in the "courses" table.
5. Update the grade of an enrollment in the "enrollments" table.
6. Commit the transaction if all updates are successful.
7. If any error occurs during the transaction, roll back the transaction.

## Exercise 4: Implement a transaction with savepoints
Create a Java program that demonstrates the use of savepoints within a transaction. The program should allow you to rollback to a specific savepoint if an error occurs, while preserving the changes made before that savepoint. The program should perform the following steps:

1. Establish a connection to the database.
2. Disable auto-commit mode to start a transaction.
3. Perform a series of updates on a table or multiple tables.
4. Set a savepoint after a specific update.
5. Perform additional updates.
6. Set another savepoint.
7. Perform a final update that will cause an error.
8. Rollback the transaction to the second savepoint and commit the changes up to that point.

## Exercise 5: Implement a nested transaction

Write a Java program that demonstrates the use of nested transactions. The program should allow you to perform a set of operations within a nested transaction, and rollback or commit the nested transaction independently from the parent transaction. The program should perform the following steps:

1. Establish a connection to the database.
2. Disable auto-commit mode to start an outer transaction.
3. Perform an update on a table or multiple tables within the outer transaction.
4. Set a savepoint for the outer transaction.
5. Start a nested transaction by disabling auto-commit mode again.
6. Perform an update within the nested transaction.
7. Commit the nested transaction.
8. If an error occurs in the nested transaction, rollback to the savepoint set for the outer transaction.
9. Perform additional updates within the outer transaction.
10. Commit the outer transaction if all updates are successful.

---

## Starter SQL code 

## Exercise 1: Implement a fund transfer transaction

**Starter SQL (MySQL):**
```sql
CREATE DATABASE bank;
USE bank;

CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    balance DECIMAL(10, 2)
);

INSERT INTO accounts (account_id, balance) VALUES (1, 5000.00);
INSERT INTO accounts (account_id, balance) VALUES (2, 3000.00);
```

## Exercise 2: Implement a multi-table data insertion transaction

**Starter SQL (MySQL):**
```sql
CREATE DATABASE school;
USE school;

CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    age INT
);

CREATE TABLE courses (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    credits INT
);

CREATE TABLE enrollments (
    id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT,
    course_id INT,
    grade VARCHAR(2),
    FOREIGN KEY (student_id) REFERENCES students(id),
    FOREIGN KEY (course_id) REFERENCES courses(id)
);
```

## Exercise 3: Implement a multi-table data update transaction

**Starter SQL (MySQL):** *(Use the same database and tables from Exercise 2)*

## Exercise 4: Implement a transaction with savepoints

Create a Java program that demonstrates the use of savepoints within a transaction. The program should allow you to rollback to a specific savepoint if an error occurs, while preserving the changes made before that savepoint.

**Starter SQL (MySQL):**
```sql
CREATE DATABASE inventory;
USE inventory;

CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    price DECIMAL(10, 2),
    quantity INT
);

INSERT INTO products (name, price, quantity) VALUES
    ('Product A', 10.00, 100),
    ('Product B', 20.00, 50),
    ('Product C', 15.00, 75);
```

## Exercise 5: Implement a nested transaction

**Starter SQL (MySQL):** *(Use the same database and tables from Exercise 1)*
