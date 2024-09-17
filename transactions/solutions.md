# Solutions for Transactions in Java JDBC Exercises

## Exercise 1: Implement a transaction to transfer funds from one account to another

```java
import java.sql.*;

public class TransferFunds {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/bank";
        String user = "root";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            conn.setAutoCommit(false); // Disable auto-commit mode

            String sql1 = "UPDATE accounts SET balance = balance - 500 WHERE account_id = 1";
            String sql2 = "UPDATE accounts SET balance = balance + 500 WHERE account_id = 2";

            Statement stmt = conn.createStatement();
            stmt.executeUpdate(sql1);
            stmt.executeUpdate(sql2);

            conn.commit(); // Commit the transaction
            System.out.println("Transaction committed successfully.");
        } catch (SQLException e) {
            try {
                if (conn != null) {
                    conn.rollback(); // Rollback the transaction
                    System.out.println("Transaction rolled back.");
                }
            } catch (SQLException ex) {
                ex.printStackTrace();
            }
            e.printStackTrace();
        }
    }
}
```

## Exercise 2: Implement a transaction to insert data into multiple tables

```java
import java.sql.*;

public class InsertData {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/school";
        String user = "root";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            conn.setAutoCommit(false); // Disable auto-commit mode

            String sql1 = "INSERT INTO students (name, age) VALUES ('John', 20)";
            String sql2 = "INSERT INTO courses (name, credits) VALUES ('Math 101', 3)";
            String sql3 = "INSERT INTO enrollments (student_id, course_id) VALUES (1, 1)";

            Statement stmt = conn.createStatement();
            stmt.executeUpdate(sql1);
            stmt.executeUpdate(sql2);
            stmt.executeUpdate(sql3);

            conn.commit(); // Commit the transaction
            System.out.println("Transaction committed successfully.");
        } catch (SQLException e) {
            try {
                if (conn != null) {
                    conn.rollback(); // Rollback the transaction
                    System.out.println("Transaction rolled back.");
                }
            } catch (SQLException ex) {
                ex.printStackTrace();
            }
            e.printStackTrace();
        }
    }
}
```

## Exercise 3: Implement a transaction to update data across multiple tables


```java
import java.sql.*;

public class UpdateData {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/school";
        String user = "root";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            conn.setAutoCommit(false); // Disable auto-commit mode

            String sql1 = "UPDATE students SET age = 21 WHERE id = 1";
            String sql2 = "UPDATE courses SET credits = 4 WHERE id = 1";
            String sql3 = "UPDATE enrollments SET grade = 'A' WHERE student_id = 1 AND course_id = 1";

            Statement stmt = conn.createStatement();
            stmt.executeUpdate(sql1);
            stmt.executeUpdate(sql2);
            stmt.executeUpdate(sql3);

            conn.commit(); // Commit the transaction
            System.out.println("Transaction committed successfully.");
        } catch (SQLException e) {
            try {
                if (conn != null) {
                    conn.rollback(); // Rollback the transaction
                    System.out.println("Transaction rolled back.");
                }
            } catch (SQLException ex) {
                ex.printStackTrace();
            }
            e.printStackTrace();
        }
    }
}
```

## Exercise 4: Implement a transaction with savepoints

```java
import java.sql.*;

public class SavepointExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/bank";
        String user = "root";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            conn.setAutoCommit(false); // Disable auto-commit mode

            String sql1 = "UPDATE accounts SET balance = balance - 1000 WHERE account_id = 1";
            String sql2 = "UPDATE accounts SET balance = balance + 1000 WHERE account_id = 2";
            String sql3 = "UPDATE accounts SET balance = balance - 500 WHERE account_id = 1";

            Statement stmt = conn.createStatement();
            stmt.executeUpdate(sql1);

            Savepoint savepoint1 = conn.setSavepoint("SAVEPOINT1");

            stmt.executeUpdate(sql2);

            Savepoint savepoint2 = conn.setSavepoint("SAVEPOINT2");

            stmt.executeUpdate(sql3); // This will cause an exception

            conn.commit(); // Commit the transaction
            System.out.println("Transaction committed successfully.");
        } catch (SQLException e) {
            try {
                if (conn != null) {
                    conn.rollback(savepoint2); // Rollback to savepoint2
                    conn.commit(); // Commit the transaction up to savepoint2
                    System.out.println("Transaction partially committed.");
                }
            } catch (SQLException ex) {
                ex.printStackTrace();
            }
            e.printStackTrace();
        }
    }
}
```

## Exercise 5: Implement a nested transaction

```java
import java.sql.*;

public class NestedTransactionExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/bank";
        String user = "root";
        String password = "password";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            conn.setAutoCommit(false); // Disable auto-commit mode

            String sql1 = "UPDATE accounts SET balance = balance - 1000 WHERE account_id = 1";
            String sql2 = "UPDATE accounts SET balance = balance + 1000 WHERE account_id = 2";

            Statement stmt = conn.createStatement();
            stmt.executeUpdate(sql1);

            Savepoint outerSavepoint = conn.setSavepoint("OUTER");

            try {
                conn.setAutoCommit(false); // Start a nested transaction

                String sql3 = "UPDATE accounts SET balance = balance - 500 WHERE account_id = 1";
                stmt.executeUpdate(sql3);

                conn.commit(); // Commit the nested transaction
            } catch (SQLException e) {
                conn.rollback(outerSavepoint); // Rollback the nested transaction
                System.out.println("Nested transaction rolled back.");
            }

            stmt.executeUpdate(sql2);

            conn.commit(); // Commit the outer transaction
            System.out.println("Outer transaction committed successfully.");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```
