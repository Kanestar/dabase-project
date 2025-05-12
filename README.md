# Library Management System Database

A comprehensive MySQL database schema designed for managing a modern library's operations, including book management, member services, loans, reservations, and fine tracking.

## Project Description

This database system provides a robust foundation for a library management application with the following features:

### Core Features
- Book inventory management with multiple authors and categories
- Member management system
- Book lending and return tracking
- Reservation system
- Fine calculation and payment tracking
- Publisher information management

### Database Structure
The system includes the following main entities:
- **Books**: Store book information including ISBN, title, and availability
- **Authors**: Manage author details with support for multiple authors per book
- **Categories**: Organize books by genres/categories
- **Members**: Track library member information and membership status
- **Loans**: Monitor book borrowing and returns
- **Reservations**: Handle book reservation requests
- **Fines**: Manage late return penalties
- **Publishers**: Store publisher information

### Key Features
- Proper primary and foreign key constraints
- Data integrity through relationship constraints
- Audit trails with creation and update timestamps
- Status tracking for loans, reservations, and memberships
- Support for multiple authors per book
- Flexible categorization system

## Setup Instructions

### Prerequisites
- MySQL Server 5.7 or higher
- MySQL Workbench (optional, for visualization)

### Installation Steps

1. **Start MySQL Server**
   ```bash
   # For Windows
   net start mysql

   # For Linux
   sudo service mysql start

   # For macOS
   mysql.server start
   ```

2. **Login to MySQL**
   ```bash
   mysql -u your_username -p
   ```

3. **Create Database**
   ```sql
   CREATE DATABASE library_management;
   USE library_management;
   ```

4. **Import Schema**
   ```bash
   # Option 1: From command line
   mysql -u your_username -p library_management < library_management.sql

   # Option 2: From MySQL prompt
   source path/to/library_management.sql
   ```

### Verification
After importing, verify the installation by checking the tables:
```sql
USE library_management;
SHOW TABLES;
```

You should see the following tables:
- Authors
- Books
- Book_Authors
- Book_Categories
- Categories
- Publishers
- Members
- Loans
- Fines
- Reservations

## Database Relationships

### One-to-Many Relationships
- Publishers → Books
- Books → Loans
- Members → Loans
- Loans → Fines
- Members → Reservations

### Many-to-Many Relationships
- Books ↔ Authors (through Book_Authors)
- Books ↔ Categories (through Book_Categories)

## Best Practices for Use

1. **Adding New Books**
   - First add the publisher if not exists
   - Add the book details
   - Add authors if not exists
   - Link book with authors using Book_Authors table
   - Assign categories using Book_Categories table

2. **Managing Loans**
   - Check book availability before creating loan
   - Update book available_copies count
   - Monitor due dates for overdue items

3. **Handling Reservations**
   - Check current reservations before accepting new ones
   - Update reservation status when fulfilled

4. **Fine Management**
   - Calculate fines based on return_date and due_date
   - Update fine payment_status when processed

## Notes
- All tables include audit trails (created_at, updated_at)
- Proper indexing on frequently queried fields
- Cascading deletes where appropriate
- Restrict deletes where data integrity is critical 