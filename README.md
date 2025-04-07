# 💳 Bank Management System

A Java-based desktop application that simulates basic banking operations with a GUI frontend. It allows account creation, deposits, withdrawals, and transaction tracking using a MySQL backend.

---

## 📌 Features

- 🔐 Login & Signup  
- 🏦 Open Account  
- 💰 Deposit & Withdraw Money  
- 📜 View Transaction History  
- 📈 Check Account Balance  
- ⚙️ Admin Controls  
- 📆 JCalendar Date Picker Integration  
- 💾 MySQL Database Connectivity  

---

## 🛠️ Tech Stack

| Technology      | Purpose                   |
|-----------------|---------------------------|
| Java (Swing/AWT)| GUI design                |
| JDBC            | Database connection       |
| MySQL           | Backend database          |
| JCalendar       | Date selection interface  |
| IntelliJ IDEA   | Development environment   |

---

## 🗃️ Folder Structure
Bank-Management-System/
├── src/
│   └── bank/
│       ├── Login.java
│       ├── Signup.java
│       ├── Dashboard.java
│       ├── Deposit.java
│       ├── Withdraw.java
│       ├── BalanceEnquiry.java
│       └── ... (other screens)
│   └── icon/
├── out/                  # Compiled bytecode
├── mysql-connector-java-8.0.28.jar
├── jcalendar-1.4.jar
└── Bank Management System.iml


## 🧠 System Architecture

![System Architecture](A_block_diagram_in_the_digital_image_illustrates_t.png)

---

## 🔄 Application Flow Diagram

[Start] --> [Login / Signup] --> [Dashboard]
     ↓                 ↓
[Withdraw]     [Open New Account]
     ↓                 ↓
[Deposit]        [Check Balance]
     ↓                 ↓
[Transaction History] <- [Logout]

---

## 🗄️ Database Schema

### `accounts` Table

| Field         | Type         |
|---------------|--------------|
| account_id    | INT (PK)     |
| name          | VARCHAR      |
| dob           | DATE         |
| address       | TEXT         |
| account_type  | VARCHAR      |
| balance       | DOUBLE       |
| created_at    | TIMESTAMP    |

### `transactions` Table

| Field          | Type         |
|----------------|--------------|
| transaction_id | INT (PK)     |
| account_id     | INT (FK)     |
| type           | VARCHAR      |
| amount         | DOUBLE       |
| timestamp      | TIMESTAMP    |

---

🌟 Future Improvements
✅ Modern UI with JavaFX

✅ PDF statement generator

✅ Dockerized MySQL DB

✅ Email notifications and OTP-based login


