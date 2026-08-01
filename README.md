# 📚 Library Management System Database Design (Industry-Level Project)

## 🎯 Objective

Design and implement a production-ready relational database for a Library Management System using SQL and SQLite

The project demonstrates database modeling, normalization, relationships,indexing,constraints, triggers, views, and query optimization following industry best practices.

---

# 📖 Problem Statement

A modern library requires a database system capable of efficiently managing books, authors, publishers, borrowers, physical book copies, borrowing transactions, and library staff.

The system should maintain data integrity, prevent duplicate records, and support efficient querying for day-to-day library operations.

The project focuses on designing a clean, scalable, and normalized relational database.

---

# 🚀 Functional Requirements

## 1. *Authors*

Store information about every author.

Attributes:

- Author ID
- Full Name
- Country
- Date of Birth
- Biography (Optional)

---

## 2. Publishers

Store publisher details.

Attributes:

- Publisher ID
- Publisher Name
- Country
- Website
- Contact Email

---

## 3. Genres

Maintain book genres separately.

Attributes:

- Genre ID
- Genre Name

Examples:

- Fiction
- Science
- Programming
- History
- Biography

---

## 4. Books

Store general information about books.

Attributes:

- Book ID
- Title
- ISBN
- Publication Year
- Language
- Number of Pages
- Publisher

Rules:

- ISBN must be unique.
- Publication year cannot be in the future.

---

## 5. Book Authors

A book may have multiple authors, and an author may write multiple books.

Implement a Many-to-Many relationship using a junction table.

---

## 6. Book Genres

A book may belong to multiple genres.

Implement a Many-to-Many relationship.

---

## 7. Book Copies

Instead of lending abstract books, libraries lend physical copies.

Each copy should contain:

- Copy ID
- Book ID
- Barcode
- Shelf Location
- Status
- Condition

Status:

- AVAILABLE
- BORROWED
- LOST
- DAMAGED

Condition:

- NEW
- GOOD
- FAIR
- POOR

---

## 8. Borrowers

Store borrower information.

Attributes:

- Borrower ID
- Full Name
- Email
- Phone Number
- Address
- Membership Date

Rules:

- Email must be unique.

---

## 9. Library Staff

Track staff members responsible for issuing books.

Attributes:

- Staff ID
- Name
- Email
- Phone
- Role

---

## 10. Borrow Records

Track borrowing history.

Attributes:

- Borrow ID
- Copy ID
- Borrower ID
- Issued By
- Borrow Date
- Due Date
- Return Date
- Fine Amount
- Status

Status:

- BORROWED
- RETURNED
- OVERDUE
- LOST

Rules:

- Return Date must be greater than Borrow Date.
- Fine cannot be negative.

---

## 11. Audit Logs

Track database activity.

Attributes:

- Log ID
- Table Name
- Operation
- Record ID
- Timestamp

Operations:

- INSERT
- UPDATE
- DELETE

---

# 📐 Relationships

### Author ↔ Book

Many-to-Many

Implemented using:

Book_Authors

---

### Genre ↔ Book

Many-to-Many

Implemented using:

Book_Genres

---

### Publisher → Books

One Publisher

↓

Many Books

---

### Book → Book Copies

One Book

↓

Many Copies

---

### Borrower → Borrow Records

One Borrower

↓

Many Borrow Records

---

### Book Copy → Borrow Records

One Copy

↓

Many Borrow Records

---

### Staff → Borrow Records

One Staff Member

↓

Many Borrow Records

---

# 🗂 Database Tables

- Authors
- Publishers
- Genres
- Books
- Book_Authors
- Book_Genres
- Book_Copies
- Borrowers
- Staff
- Borrow_Records
- Audit_Logs

Total Tables: **11**

---

# 🔒 Constraints

The database should enforce the following constraints:

- Primary Keys
- Foreign Keys
- NOT NULL
- UNIQUE
- CHECK
- DEFAULT
- ON DELETE CASCADE
- ON UPDATE CASCADE

Examples:

- ISBN must be unique.
- Borrower email must be unique.
- Publication year cannot exceed current year.
- Fine amount cannot be negative.
- Return date cannot be earlier than borrow date.

---

# ⚡ Indexes

Create indexes for frequently searched columns.

Suggested indexes:

- ISBN
- Book Title
- Author Name
- Borrower Email
- Borrow Date
- Book Status

---

# 🔄 Triggers

Implement triggers for automatic database operations.

Examples:

### Borrow Trigger

When a book copy is borrowed:

AVAILABLE

↓

BORROWED

---

### Return Trigger

When a book is returned:

BORROWED

↓

AVAILABLE

---

### Audit Trigger

Automatically insert logs into Audit_Logs after every INSERT, UPDATE, and DELETE.

---

# 👀 Database Views

Create reusable SQL views.

### Available_Books

Display all books currently available.

---

### Borrow_History

Complete borrowing history.

---

### Overdue_Books

Show all overdue books.

---

### Most_Borrowed_Books

Display the most borrowed books.

---

# 🧠 Normalization

The database must satisfy:

- First Normal Form (1NF)
- Second Normal Form (2NF)
- Third Normal Form (3NF)
- Boyce-Codd Normal Form (BCNF)

---

# 📊 Sample Data

Populate the database with realistic sample data.

Suggested dataset:

- 20 Authors
- 10 Publishers
- 15 Genres
- 100 Books
- 300 Book Copies
- 50 Borrowers
- 10 Staff Members
- 200 Borrow Records

---

# 💻 SQL Tasks

## Basic Queries

- List all books
- List all authors
- Find books by genre
- Search by ISBN

---

## Intermediate Queries

- Books by a specific author
- Borrow history of a borrower
- Available books
- Current borrowed books
- Books never borrowed

---

## Advanced Queries

- Top 10 most borrowed books
- Top active borrowers
- Monthly borrowing statistics
- Genre-wise borrowing count
- Ranking books using Window Functions
- CTE-based reports

---

# 📂 Project Structure

library-management-db/

├── README.md

├── schema/

│ ├── 01_tables.sql

│ ├── 02_constraints.sql

│ ├── 03_indexes.sql

│ ├── 04_triggers.sql

│ ├── 05_views.sql

│

├── seed/

│ └── seed.sql

│

├── queries/

│ ├── beginner_queries.sql

│ ├── intermediate_queries.sql

│ └── advanced_queries.sql

│

├── docs/

│ ├── ERD.png

│ ├── Database_Design.md

│ ├── Normalization.md

│ └── Assumptions.md

│

└── images/

└── er_diagram.png

---

# ⭐ Bonus Features

- Prevent double borrowing of the same book copy.
- Automatic overdue detection.
- Automatic fine calculation.
- Soft delete support.
- Audit logging using triggers.
- Optimized indexes for faster searching.
- Database views for reporting.
- Fully normalized schema.

---

# 🛠 Installation & Setup

## Prerequisites

- SQLite3

Verify installation:

```bash
sqlite3 --version
```

---

## Create Database

```bash
sqlite3 library.db < schema/01_tables.sql
sqlite3 library.db < schema/02_constraints.sql
sqlite3 library.db < schema/03_indexes.sql
sqlite3 library.db < schema/04_triggers.sql
sqlite3 library.db < schema/05_views.sql
```

---

## Seed Data

```bash
sqlite3 library.db < seed/seed.sql
```

---

## Verify

```sql
SELECT * FROM Authors;

SELECT * FROM Books LIMIT 10;

SELECT * FROM Borrow_Records;

SELECT * FROM Available_Books;

SELECT * FROM Overdue_Books;
```

---

# 🎯 Learning Outcomes

After completing this project, students will understand:

- Relational Database Design
- Entity Relationship Modeling
- Database Normalization
- Primary & Foreign Keys
- Many-to-Many Relationships
- Constraints
- Indexing
- Views
- Triggers
- Query Optimization
- SQL Best Practices

---

# 📌 Future Scope

- Spring Boot REST API
- React Dashboard
- JWT Authentication
- Docker Deployment
- PostgreSQL Migration
- Redis Caching
- Role-Based Access Control
- Email Notifications
- Fine Payment System
- Book Reservation Module
