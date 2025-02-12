# MySQL Database Setup for XpensePro

## 1️⃣ Install MySQL on EC2
To install MySQL on an AWS EC2 instance (amazon AMI-based):
```bash
sudo apt update
sudo apt install mysql-server -y


##Start MySQL service:
sudo systemctl start mysql

2️⃣ Secure MySQL Installation
sudo mysql_secure_installation

3️⃣ Create Database & User
After logging into MySQL:

CREATE DATABASE xpensepro_db;
CREATE USER 'xpenseuser'@'localhost' IDENTIFIED BY 'XpenseUser@123';
GRANT ALL PRIVILEGES ON xpensepro_db.* TO 'xpenseuser'@'localhost';
FLUSH PRIVILEGES;
###Verify database and user creation:

SHOW DATABASES;
SELECT User FROM mysql.user;



####completed mysql installation data if you need backup we can follow these 


4️⃣ Take a Database Backup
To create a backup of the database:

mysqldump -u root -p xpensepro_db > xpensepro_db_backup.sql

##Confirm the file is created:
ls -l xpensepro_db_backup.sql


5️⃣ Transfer Backup to Local Machine
Using SCP to securely copy the backup file from EC2 to our local system:

scp -i linux-key.pem ec2-user@<your-ec2-public-ip>:~/xpensepro/xpensepro_db_backup.sql .

Verify the file is downloaded:

ls -l xpensepro_db_backup.sql



6️⃣ Push Backup to GitHub
After confirming the backup is safe, we added it to GitHub for version control:
git init
git add xpensepro_db_backup.sql
git commit -m "Added MySQL database backup"
git push origin master


✅ Summary
✔️ MySQL Installed on EC2
✔️ Database (xpensepro_db) and User (xpenseuser) Created
✔️ Database Backup Taken (xpensepro_db_backup.sql)
✔️ Backup Transferred to Local Machine
✔️ Backup Pushed to GitHub

Save and Commit the Documentation
Once you've added this content in VS Code, save the file (Ctrl + S) and commit it to GitHub:

bash
Copy
Edit
cd /c/devops-project
git add mysql_setup.md
git commit -m "Added MySQL setup documentation"
git push origin master



# **Day-3 Documentation: MySQL Setup on AWS EC2 & Troubleshooting**

## **Overview**
Today, we successfully completed the MySQL database setup on an AWS EC2 instance, restored a database backup, and resolved various issues related to authentication, permissions, and SCP file transfer.

---
## **1️⃣ Steps Completed**
### **Step 1: Connect to AWS EC2 Instance**
- We used an SSH key pair to securely connect to the AWS EC2 instance.
- Verified the connection and ensured the key was in place.

**Command Used:**
```bash
ssh -i linuxkeynew.pem ec2-user@<EC2-Public-IP>
```

### **Step 2: Install & Configure MySQL (MariaDB)**
- Updated the system packages.
- Installed MariaDB (MySQL-compatible).
- Started and enabled the MariaDB service.

**Commands Used:**
```bash
sudo yum update -y
sudo yum install -y mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

### **Step 3: Secure MySQL**
- Removed anonymous users.
- Disabled remote root login.
- Removed the test database.

**Command Used:**
```bash
sudo mysql_secure_installation
```

### **Step 4: Verify MySQL Login & Authentication**
- Checked authentication method.
- Confirmed that MySQL was using `mysql_native_password`.

**Commands Used:**
```sql
SELECT user, host, plugin FROM mysql.user;
```

### **Step 5: Transfer Database Backup File**
- Used `scp` to securely copy the backup file from the local machine to EC2.

**Command Used:**
```bash
scp -i linuxkeynew.pem xpensepro_db_backup.sql ec2-user@<EC2-Public-IP>:~/
```

### **Step 6: Restore the Database from Backup**
- Logged into MySQL and restored the backup.

**Commands Used:**
```bash
mysql -u root -p
```
Inside MySQL:
```sql
SOURCE xpensepro_db_backup.sql;
SHOW DATABASES;
USE xpensepro_db;
SHOW TABLES;
SELECT * FROM users;
```

---
## **2️⃣ Issues Faced & Solutions**

### **Issue 1: SCP File Transfer Failed (Permission Denied)**
✅ **Solution:**
- Ensured the `.pem` key was present and had the correct permissions.
- Used the correct path and retried the SCP command.

```bash
chmod 400 linuxkeynew.pem
scp -i linuxkeynew.pem xpensepro_db_backup.sql ec2-user@<EC2-Public-IP>:~/
```

### **Issue 2: MySQL Root Access Denied (ERROR 1698)**
✅ **Solution:**
- Logged in as a `sudo` user instead of using a password.

```bash
sudo mysql
```

### **Issue 3: Database Restore Not Showing Tables**
✅ **Solution:**
- Verified the database exists.
- Used `USE xpensepro_db;` and `SHOW TABLES;` to confirm restoration.

```sql
SHOW DATABASES;
USE xpensepro_db;
SHOW TABLES;
```

---
## **3️⃣ Final Verification**
✅ **Ensured MySQL service is running**
```bash
sudo systemctl status mariadb
```
✅ **Checked the restored database and tables**
```sql
SHOW DATABASES;
USE xpensepro_db;
SHOW TABLES;
SELECT * FROM users;
```
✅ **Confirmed successful SSH, SCP, and MySQL setup.**

---
## **4️⃣ Summary**
📌 Today, we successfully:
- Connected to AWS EC2 instance securely.
- Installed & configured MySQL.
- Secured MySQL and verified authentication.
- Transferred and restored a database backup.
- Resolved permission and access issues.
- Validated the database contents.

💡 **Next Step:** Backend setup for database integration!

---
### **Prepared By:** Vamsi
📅 **Date:** February 6, 2025

