
# 🛡️ Secure Online Event Booking (PHP + MySQL)

## 🌐 Project Overview

This project is a secure web-based **Online Event Booking** system built with **PHP** and **MySQL**, hosted on [InfinityFree](https://infinityfree.net). It demonstrates how common web vulnerabilities can be introduced—and then mitigated—within a real-world web application. The main functionalities include:

- User registration and login
- Role-based access (admin and user)
- Dashboard for users
- Admin panel
- Secure password storage
- SQL Injection and XSS protection examples

🔗 **Live demo**: [https://sarah.great-site.net](https://sarah.great-site.net)

---

## ⚙️ How to Run the Application Locally

1. **Install XAMPP** or any local PHP server with MySQL.
2. Clone this repository:
   ```bash
   git clone https://github.com/your-username/secure-event-booking.git
   cd secure-event-booking
   ```
3. Import the database:
   - Open **phpMyAdmin**.
   - Create a database named `online_event_booking`.
   - Import the `online_event_booking.sql` file provided in the repo.
4. Update your `config.php` (local version):
   ```php
   $host = 'localhost';
   $user = 'root';
   $password = '';
   $db = 'online_event_booking';
   $port = 3306;
   ```
5. Launch the app by visiting:  
   `http://localhost/index.php`

---

## ☁️ Remote Hosting Info (InfinityFree)

- **Username**: `if0_38940288`
- **Domain**: [https://sarah.great-site.net](https://sarah.great-site.net)
- **Database Host**: `sql101.infinityfree.com`
- **Database Name**: `if0_38940288_Online_Event_Booking`
- **Database User**: `if0_38940288`

Ensure your `config.php` is updated with InfinityFree's credentials when deployed.

---

## 🔐 How to Test Security Features

### 1. 🧨 SQL Injection

- Go to the **login page**.
- Try entering:
  ```sql
  Username: ' OR 1=1 --
  Password: anything
  ```
- This **used to work** before mitigation.
- Now, it **fails** due to the use of **prepared statements** in `login.php`.

---

### 2. 🔓 Weak Password Storage

- Initially, passwords were stored using `md5()`.
- Now replaced with:
  ```php
  password_hash($password, PASSWORD_BCRYPT);
  ```
- Verified securely on login using `password_verify()`.

---

### 3. 💥 XSS Prevention

- Go to `dashboard.php`.
- Try submitting:
  ```html
  <script>alert('Hacked!');</script>
  ```
- This **will be escaped**, and the script will **not run**.
- Mitigation is done using `htmlspecialchars()`.

---

### 4. 🚫 Role-Based Access Control

- Try accessing `admin.php` directly from the browser after logging in as a normal user.
- You’ll get an **access denied** message.
- Admins are verified using:
  ```php
  $_SESSION['is_admin'] == 1
  ```

---

### 5. 🔐 Encryption and HTTPS

- Passwords are encrypted using **bcrypt**.
- Site uses **InfinityFree’s free SSL** to serve pages over **HTTPS**.
- Optional HTTPS enforcement available in `config.php`.

---

## 📁 Key Files

| File         | Purpose                            |
|--------------|-------------------------------------|
| `index.php`  | Entry point (home or redirect)      |
| `login.php`  | User login + SQLi protection        |
| `register.php` | User signup + secure password hash |
| `dashboard.php` | XSS test + user content display   |
| `admin.php`  | RBAC demonstration (admin-only)     |
| `logout.php` | Secure session destroy              |
| `config.php` | DB connection + helper functions    |
| `online_event_booking.sql` | Database structure + sample data |

---

## Authors
**Sarah Alkhayyal**  
**Reema Alshwirekh** 
**Renad Aldayel** 
**Bushra Alkhudhyr** 
InfinityFree user: `if0_38940288`  
Live site: [https://sarah.great-site.net](https://sarah.great-site.net)

---
