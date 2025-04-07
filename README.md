# 🏦 Bank Management System

A comprehensive Java-based desktop application that simulates a real-world banking environment with a graphical user interface. The system allows users to create accounts, perform banking operations like deposits and withdrawals, and track transaction history using a MySQL database backend.

[![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)](https://www.java.com/)
[![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![JDBC](https://img.shields.io/badge/JDBC-007396?style=for-the-badge&logo=java&logoColor=white)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/)
[![Swing](https://img.shields.io/badge/Swing-007396?style=for-the-badge&logo=java&logoColor=white)](https://docs.oracle.com/javase/tutorial/uiswing/)

## 📋 Table of Contents
- [Features](#-features)
- [Screenshots](#-screenshots)
- [System Requirements](#-system-requirements)
- [Installation & Setup](#-installation--setup)
- [Tech Stack](#-tech-stack)
- [System Architecture](#-system-architecture)
- [Application Flow](#-application-flow)
- [Database Schema](#-database-schema)
- [Folder Structure](#-folder-structure)
- [Usage Guide](#-usage-guide)
- [Future Improvements](#-future-improvements)
- [Contributing](#-contributing)
- [License](#-license)

## 📌 Features

- **User Authentication**
  - 🔐 Secure login system
  - 👤 New user registration
  - 🔑 Password management
  
- **Account Management**
  - 🏦 Create new bank accounts (Savings/Current/Fixed Deposit)
  - 📝 Update account information
  - 🗑️ Close existing accounts
  
- **Transaction Operations**
  - 💰 Deposit funds
  - 💸 Withdraw money
  - 🔄 Fund transfers between accounts
  - 📜 View detailed transaction history
  
- **Utility Functions**
  - 📊 Balance enquiry
  - 📈 Financial summary
  - 📅 Transaction date filtering using JCalendar
  
- **Administrative Tools**
  - 👨‍💼 Admin dashboard
  - 👥 User management
  - 📊 System statistics

## 📸 Screenshots

<div align="center">
  <img src="/screenshots/login.png" alt="Login Screen" width="300"/>
  <img src="/screenshots/dashboard.png" alt="Dashboard" width="300"/>
  <img src="/screenshots/transaction.png" alt="Transaction Screen" width="300"/>
</div>

## 💻 System Requirements

- **Java Development Kit (JDK)**: Version 8 or higher
- **MySQL**: Version 5.7 or higher
- **RAM**: Minimum 2GB (4GB recommended)
- **Storage**: 100MB free disk space
- **OS**: Windows 7/8/10, macOS 10.12+, or Linux

## 🚀 Installation & Setup

### Prerequisites
1. Install JDK 8 or higher
2. Install MySQL Server
3. Configure MySQL user credentials

### Database Setup
```sql
CREATE DATABASE bank_management;
USE bank_management;

CREATE TABLE accounts (
  account_id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100) NOT NULL,
  dob DATE,
  address TEXT,
  phone VARCHAR(15),
  email VARCHAR(50),
  account_type VARCHAR(20),
  balance DOUBLE DEFAULT 0.0,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE transactions (
  transaction_id INT PRIMARY KEY AUTO_INCREMENT,
  account_id INT,
  type VARCHAR(20),
  amount DOUBLE,
  timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (account_id) REFERENCES accounts(account_id)
);

CREATE TABLE users (
  user_id INT PRIMARY KEY AUTO_INCREMENT,
  username VARCHAR(50) UNIQUE,
  password VARCHAR(255),
  is_admin BOOLEAN DEFAULT FALSE,
  account_id INT,
  FOREIGN KEY (account_id) REFERENCES accounts(account_id)
);
```

### Application Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/ashuuu14/Bank-Management-System.git
   ```
2. Open the project in IntelliJ IDEA or your preferred IDE
3. Add the following JAR files to your project's classpath:
   - `mysql-connector-java-8.0.28.jar`
   - `jcalendar-1.4.jar`
4. Configure database connection in the application:
   - Update `src/bank/DatabaseConnect.java` with your MySQL credentials
5. Build and run the application

## 🛠️ Tech Stack

| Technology        | Purpose                                   |
|-------------------|-------------------------------------------|
| Java              | Core programming language                 |
| Swing & AWT       | GUI components and layout management      |
| JDBC              | Database connectivity and operations      |
| MySQL             | Relational database management system     |
| JCalendar Library | Date picker component for date selection  |
| IntelliJ IDEA     | Integrated development environment        |

## 🧠 System Architecture

The Bank Management System follows a three-tier architecture:

```
┌───────────────────┐      ┌───────────────────┐      ┌───────────────────┐
│                   │      │                   │      │                   │
│  Presentation     │      │    Business       │      │     Data          │
│  Layer (GUI)      │◄────►│    Logic Layer    │◄────►│     Access Layer  │
│                   │      │                   │      │                   │
└───────────────────┘      └───────────────────┘      └───────────────────┘
                                                             │
                                                             ▼
                                                      ┌───────────────────┐
                                                      │                   │
                                                      │     MySQL         │
                                                      │     Database      │
                                                      │                   │
                                                      └───────────────────┘
```

### Layer Descriptions:

1. **Presentation Layer**: Swing/AWT-based GUI components for user interaction
2. **Business Logic Layer**: Core application logic, transaction processing, and validations
3. **Data Access Layer**: JDBC implementation for database operations
4. **Database**: MySQL-based persistent storage

## 🔄 Application Flow

```
                           ┌──────────────┐
                           │    Start     │
                           └──────┬───────┘
                                  │
                                  ▼
                    ┌─────────────────────────┐
                    │      Login/Signup       │
                    └──────────┬──────────────┘
                               │
                               ▼
                    ┌─────────────────────────┐
                    │       Dashboard         │
                    └─┬─────────┬───────┬─────┘
                      │         │       │
           ┌──────────┘    ┌────┘       └────┐
           │               │                 │
           ▼               ▼                 ▼
┌────────────────┐ ┌────────────────┐ ┌────────────────┐
│   Withdraw     │ │  Open Account  │ │  Check Balance │
└───────┬────────┘ └────────┬───────┘ └───────┬────────┘
        │                   │                 │
        ▼                   ▼                 │
┌────────────────┐ ┌────────────────┐         │
│    Deposit     │ │ Update Account │         │
└───────┬────────┘ └────────┬───────┘         │
        │                   │                 │
        └───────────────────┼─────────────────┘
                            │
                            ▼
                  ┌─────────────────────────┐
                  │   Transaction History   │
                  └─────────────┬───────────┘
                                │
                                ▼
                         ┌─────────────┐
                         │   Logout    │
                         └─────────────┘
```

## 🗄️ Database Schema

### Entity-Relationship Diagram

```
┌────────────────────┐       ┌────────────────────┐       ┌────────────────────┐
│      accounts      │       │    transactions    │       │       users        │
├────────────────────┤       ├────────────────────┤       ├────────────────────┤
│ PK: account_id     │◄──────┤ FK: account_id     │       │ PK: user_id        │
│     name           │       │ PK: transaction_id │       │     username       │
│     dob            │       │     type           │       │     password       │
│     address        │       │     amount         │       │     is_admin       │
│     phone          │       │     timestamp      │       │ FK: account_id     │────┐
│     email          │       │                    │       │                    │    │
│     account_type   │       └────────────────────┘       └────────────────────┘    │
│     balance        │                                                              │
│     created_at     │◄─────────────────────────────────────────────────────────────┘
└────────────────────┘
```

### Table Schemas

#### `accounts` Table

| Field         | Type         | Constraints      | Description                     |
|---------------|--------------|------------------|---------------------------------|
| account_id    | INT          | PK, AUTO_INCREMENT | Unique identifier               |
| name          | VARCHAR(100) | NOT NULL         | Account holder's name           |
| dob           | DATE         |                  | Date of birth                   |
| address       | TEXT         |                  | Residential address             |
| phone         | VARCHAR(15)  |                  | Contact number                  |
| email         | VARCHAR(50)  |                  | Email address                   |
| account_type  | VARCHAR(20)  |                  | Savings/Current/Fixed Deposit   |
| balance       | DOUBLE       | DEFAULT 0.0      | Current account balance         |
| created_at    | TIMESTAMP    | DEFAULT CURRENT_TIMESTAMP | Account creation date   |

#### `transactions` Table

| Field          | Type         | Constraints      | Description                     |
|----------------|--------------|------------------|---------------------------------|
| transaction_id | INT          | PK, AUTO_INCREMENT | Unique identifier               |
| account_id     | INT          | FK               | Reference to accounts table     |
| type           | VARCHAR(20)  |                  | Deposit/Withdrawal/Transfer     |
| amount         | DOUBLE       |                  | Transaction amount              |
| timestamp      | TIMESTAMP    | DEFAULT CURRENT_TIMESTAMP | Transaction date and time |

#### `users` Table

| Field         | Type         | Constraints      | Description                     |
|---------------|--------------|------------------|---------------------------------|
| user_id       | INT          | PK, AUTO_INCREMENT | Unique identifier               |
| username      | VARCHAR(50)  | UNIQUE           | Login username                  |
| password      | VARCHAR(255) |                  | Encrypted password              |
| is_admin      | BOOLEAN      | DEFAULT FALSE    | Administrator flag              |
| account_id    | INT          | FK               | Reference to accounts table     |

## 📂 Folder Structure

```
Bank-Management-System/
├── src/
│   ├── bank/
│   │   ├── authentication/
│   │   │   ├── Login.java         # Login screen
│   │   │   └── Signup.java        # Registration screen
│   │   ├── ui/
│   │   │   ├── Dashboard.java     # Main dashboard
│   │   │   ├── AccountCreation.java
│   │   │   ├── Deposit.java
│   │   │   ├── Withdraw.java
│   │   │   ├── BalanceEnquiry.java
│   │   │   └── TransactionHistory.java
│   │   ├── models/
│   │   │   ├── Account.java       # Account data model
│   │   │   ├── Transaction.java   # Transaction data model
│   │   │   └── User.java          # User data model
│   │   ├── dao/
│   │   │   ├── AccountDAO.java    # Account database operations
│   │   │   ├── TransactionDAO.java
│   │   │   └── UserDAO.java
│   │   ├── util/
│   │   │   ├── DatabaseConnect.java
│   │   │   └── DateUtils.java
│   │   └── Main.java              # Application entry point
│   └── resources/
│       ├── images/
│       │   ├── logo.png
│       │   ├── background.jpg
│       │   └── icons/
│       └── config.properties
├── lib/                           # External libraries
│   ├── mysql-connector-java-8.0.28.jar
│   └── jcalendar-1.4.jar
├── docs/                          # Documentation
│   ├── user-manual.pdf
│   └── developer-guide.md
├── sql/
│   └── schema.sql                 # Database creation script
├── out/                           # Compiled bytecode
├── test/                          # Unit tests
├── screenshots/                   # UI screenshots
├── .gitignore
├── README.md
└── Bank Management System.iml
```

## 📋 Usage Guide

### User Access
1. **Login**: Existing users can log in with username and password
2. **Signup**: New users can register with personal details

### Banking Operations
1. **Creating an Account**:
   - Navigate to "Open Account" from dashboard
   - Fill in personal details and select account type
   - Submit to generate new account number

2. **Deposits**:
   - Select "Deposit" from dashboard
   - Enter account number and deposit amount
   - Confirm transaction

3. **Withdrawals**:
   - Select "Withdraw" from dashboard
   - Enter account number and withdrawal amount
   - System validates available balance before processing

4. **Balance Enquiry**:
   - Select "Balance Enquiry" from dashboard
   - Enter account number to view current balance

5. **Transaction History**:
   - Select "Transaction History" from dashboard
   - Enter account number
   - Optional: Filter by date range using JCalendar

## 🌟 Future Improvements

- **Technical Enhancements**
  - ✅ Migration to JavaFX for modern UI experience
  - ✅ Implementation of RESTful API for mobile app integration
  - ✅ Containerization with Docker for easy deployment
  - ✅ Integration with Spring Framework

- **Feature Additions**
  - ✅ PDF statement generator and email delivery
  - ✅ OTP-based transaction verification
  - ✅ Biometric authentication support
  - ✅ Loan management module
  - ✅ Investment portfolio tracking

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

<div align="center">
  <b>Developed with ❤️ by [Your Name]</b><br>
  <i>For any inquiries, please reach out at: your.email@example.com</i>
</div>
