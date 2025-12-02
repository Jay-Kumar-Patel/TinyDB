# TinyDB

TinyDB is a prototype of a light-weight DBMS (Database Management System) built using Java programming language. It provides a command-line interface for database operations with user authentication, transaction support, and data export capabilities.

## Features

- **User Authentication**: Secure login/registration system with security questions and captcha verification
- **Database Management**: Create, use, and manage multiple databases
- **Table Operations**: Create tables with various data types, constraints (PRIMARY KEY, NOT NULL, UNIQUE), and foreign keys
- **Data Manipulation**: Support for INSERT, SELECT, UPDATE, and DELETE queries
- **Transaction Support**: ACID-compliant transactions with COMMIT and ROLLBACK
- **Data Export**: Export database structure and data as SQL dump files
- **ERD Generation**: Generate Entity Relationship Diagrams for database visualization
- **Logging System**: Comprehensive logging of all operations and events

## Initial Command Line Interface

When you first run the application, you'll see a menu with the following options:

```
Menu:
1. Login
2. Register
3. Exit
```

Choose an option to either register as a new user, login as an existing user, or exit from the system.

## User Registration

- Registering a new user requires:
  - **Username**
  - **Password**
  - **Security Questions**
  - **Captcha Verification**

### Storing User Data

- User data is stored in `DataStore/User_Profile.txt`
- Passwords are hashed using MD5 algorithm before storage
- Security questions and answers are also stored securely
- Once a user successfully logs in, logs of that user are added to `DataStore/logs/` directory

## Main Menu

After successful login, users can access the following options:

```
1. Write Queries
2. Export Data and Structure
3. ERD
4. Go back
```

## SQL Queries

### Database Operations

#### Create Database

```sql
CREATE DATABASE database_name;
```

#### Use Database

```sql
USE database_name;
```

### Table Operations

#### Create Table

The CREATE TABLE syntax is similar to MySQL syntax. You can specify:

- Column names and data types (INT, FLOAT, STRING, DATE, BOOLEAN, DOUBLE, VARCHAR)
- Constraints: PRIMARY KEY, NOT NULL, UNIQUE
- Foreign keys (defined interactively after table creation)

Example:

```sql
CREATE TABLE employee (id INT PRIMARY KEY, name VARCHAR(255) NOT NULL, email VARCHAR(255) UNIQUE);
```

After creating a table, the system will prompt you to add foreign keys if needed.

### Data Manipulation

#### Insert Queries

```sql
INSERT INTO table_name VALUES ('value1', 'value2', 'value3');
```

Or with specific columns:

```sql
INSERT INTO table_name (column1, column2) VALUES ('value1', 'value2');
```

#### Select Queries

Select all columns:

```sql
SELECT * FROM table_name;
```

Select specific columns:

```sql
SELECT column1, column2 FROM table_name;
```

Select with WHERE clause:

```sql
SELECT * FROM table_name WHERE column_name = 'value';
```

#### Update Queries

```sql
UPDATE table_name SET column_name = 'new_value' WHERE condition_column = 'condition_value';
```

#### Delete Queries

Delete with condition:

```sql
DELETE FROM table_name WHERE column_name = 'value';
```

#### Drop Table

```sql
DROP TABLE table_name;
```

### Transaction Support

TinyDB supports ACID-compliant transactions:

#### Start Transaction

```sql
START TRANSACTION;
```

#### Commit Transaction

```sql
COMMIT;
```

#### Rollback Transaction

```sql
ROLLBACK;
```

All queries executed between START TRANSACTION and COMMIT/ROLLBACK are treated as a single atomic operation.

## Export Data and Structure

- Users can export a database to a SQL dump file
- The export includes:
  - CREATE TABLE statements with all constraints
  - INSERT statements for all data
- Exported files are saved in `DataStore/{database_name}/Export/` directory
- Files are timestamped for easy identification

## ERD (Entity Relationship Diagram)

- Generate Entity Relationship Diagrams for your databases
- Visualizes:
  - All tables in the database
  - Relationships between tables (foreign keys)
  - Cardinality of relationships
- ERD is displayed in the console

## Data Storage

- All databases are stored in the `DataStore/` directory
- Each database has its own folder containing:
  - Schema file (`{database_name}.txt`)
  - Table data files (`{table_name}.txt`)
  - Export directory (for SQL dumps)

## Logging

- All operations are logged in `DataStore/logs/` directory
- Logs include:
  - Successful operations with execution time
  - Failed operations with error messages
  - User login/logout events
  - Query execution details

## Supported Data Types

- **INT**: Integer values
- **FLOAT**: Floating-point numbers
- **DOUBLE**: Double-precision floating-point numbers
- **STRING**: String values
- **VARCHAR**: Variable-length character strings (with optional size)
- **DATE**: Date values
- **BOOLEAN**: Boolean values (true/false)

## Constraints

- **PRIMARY KEY**: Uniquely identifies each row
- **NOT NULL**: Ensures column cannot have NULL values
- **UNIQUE**: Ensures all values in column are unique
- **FOREIGN KEY**: Establishes relationships between tables

## Project Structure

```
TinyDB/
├── src/main/java/com/csci5408/
│   ├── Authentication/      # User authentication and session management
│   ├── Engine/              # Core database engine and query processing
│   ├── Export/              # Database export and ERD generation
│   ├── Models/              # Data models and enums
│   ├── OS/                  # File operations, I/O, and logging
│   └── Utils/               # Utility classes and exceptions
├── DataStore/               # Database storage directory (created at runtime)
└── pom.xml                  # Maven configuration
```

## Notes

- The system uses file-based storage (not a full database server)
- SQL syntax is similar to MySQL but with some limitations
- All data is persisted to disk in text format
- Transactions create temporary copies of the database for rollback capability
