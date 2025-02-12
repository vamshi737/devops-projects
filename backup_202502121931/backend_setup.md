<<<<<<< HEAD
📌 Backend Setup Documentation - backend_setup.md
markdown
Copy
Edit
# 🚀 Backend Setup for XpensePro

## **1️⃣ Backend Environment Setup**
### **Step 1: Connect to EC2 Instance**
```bash
ssh -i your-key.pem ec2-user@your-ec2-public-ip
Step 2: Install Node.js & NPM
bash
Copy
Edit
sudo yum update -y
sudo yum install -y nodejs npm
Step 3: Initialize Backend Project
bash
Copy
Edit
mkdir xpensepro-backend && cd xpensepro-backend
npm init -y
2️⃣ Install Required Dependencies
bash
Copy
Edit
npm install express mysql
3️⃣ Creating index.js File
javascript
Copy
Edit
const express = require("express");
const mysql = require("mysql");

const app = express();
const PORT = 3000;

// MySQL Database Connection
const db = mysql.createConnection({
    host: "172.31.46.9", // MySQL Private IP
    user: "root",
    password: "Xpensepro@123",
    database: "xpensepro"
});

db.connect((err) => {
    if (err) {
        console.error("Database connection failed: " + err.stack);
        return;
    }
    console.log("Connected to MySQL successfully!");
});

app.get("/", (req, res) => {
    res.send("XpensePro Backend is running!");
});

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
4️⃣ MySQL Database Setup
Step 1: Start MySQL & Login
bash
Copy
Edit
sudo systemctl restart mariadb
mysql -u root -p
Step 2: Create Database
sql
Copy
Edit
CREATE DATABASE xpensepro;
SHOW DATABASES;
Step 3: Grant User Permissions
sql
Copy
Edit
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'Xpensepro@123' WITH GRANT OPTION;
FLUSH PRIVILEGES;
EXIT;
5️⃣ Running the Backend Server
bash
Copy
Edit
cd ~/xpensepro-backend
node index.js
🛑 Issues Faced & Solutions
Issue 1: Access Denied for user 'root'@'localhost'
🔹 Cause:
MySQL was using unix_socket authentication.
✅ Solution:
sql
Copy
Edit
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Xpensepro@123';
FLUSH PRIVILEGES;
Issue 2: MySQL Connection Failing in Backend
🔹 Cause:
MySQL was only accessible from localhost.
✅ Solution:
Change the host in index.js to MySQL Private IP.
Issue 3: EADDRINUSE: Address Already in Use
🔹 Cause:
The backend server was already running on port 3000.
✅ Solution:
Find and kill the process using port 3000:
bash
Copy
Edit
sudo lsof -i :3000
sudo kill -9 <PID>
Issue 4: Unable to Access Backend from Browser
🔹 Cause:
Security Group did not allow inbound rules for port 3000.
✅ Solution:
Add an inbound rule in AWS Security Group:
Type: Custom TCP Rule
Port: 3000
Source: 0.0.0.0/0
6️⃣ Final Testing
Test MySQL Connection
bash
Copy
Edit
mysql -u root -p -h 172.31.46.9
Test Backend API
bash
Copy
Edit
curl http://your-ec2-public-ip:3000
✅ Expected Output:

arduino
Copy
Edit
XpensePro Backend is running!
7️⃣ Push to GitHub
bash
Copy
Edit
git init
git add backend_setup.md
git commit -m "Added backend setup documentation"
git remote add origin <your-github-repo-url>
git branch -M main
git push -u origin main
8️⃣ Stop the EC2 Instance (To Save Free Tier Usage)
bash
Copy
Edit
aws ec2 stop-instances --instance-ids <your-instance-id>
=======
# Backend Setup Documentation
>>>>>>> 341487e (Recreating backend setup documentation)
