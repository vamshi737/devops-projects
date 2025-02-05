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