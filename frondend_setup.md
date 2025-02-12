# Frontend Setup & Issues Faced

## **📌 Steps Completed Today**

### ✅ **1. Setup Frontend on EC2**
- Connected to EC2 using MobaXterm.
- Navigated to the project folder `xpensepro-frontend`.
- Installed all dependencies using:
  ```bash
  npm install --legacy-peer-deps
  ```

### ✅ **2. Fixed Installation & Dependency Errors**
- Encountered `package.json` missing errors.
- Manually removed and reinstalled dependencies:
  ```bash
  rm -rf node_modules package-lock.json
  npm cache clean --force
  npm install --legacy-peer-deps
  ```

### ✅ **3. Started Frontend using PM2**
- Installed `pm2` process manager:
  ```bash
  npm install -g pm2
  ```
- Started frontend in background:
  ```bash
  pm2 start npm --name "xpensepro-frontend" -- start
  ```
- Verified that PM2 is running:
  ```bash
  pm2 list
  ```

### ✅ **4. Fixed Missing Module Error (`web-vitals` Issue)**
- Encountered `Module not found: Can't resolve 'web-vitals'`.
- Installed missing dependency:
  ```bash
  npm install web-vitals --save
  ```
- Restarted the frontend:
  ```bash
  pm2 restart xpensepro-frontend
  ```

### ✅ **5. Checked if Frontend is Running**
- Opened the browser and verified:
  - **http://18.208.226.3:3000**
  - **http://54.208.148.142:3000**
- Frontend successfully displayed React App.

## **📌 Issues Faced & Resolutions**
| Issue | Solution |
|------|----------|
| `npm install` errors | Used `--legacy-peer-deps` flag |
| `package.json` not found | Moved to correct project directory |
| `web-vitals` module missing | Manually installed using `npm install web-vitals --save` |
| PM2 process not found | Started process manually using `pm2 start npm --name "xpensepro-frontend" -- start` |

## **📌 Next Steps**
1️⃣ **Backend Setup on EC2**
2️⃣ **API Integration Between Frontend & Backend**
3️⃣ **Testing API Calls**
4️⃣ **Fixing Any Additional Issues**
5️⃣ **Final Deployment**

## **📌 Important Commands**
```bash
# Start frontend
pm start

# Start frontend using PM2
pm2 start npm --name "xpensepro-frontend" -- start

# Restart PM2 process
pm2 restart xpensepro-frontend

# Check if PM2 is running
pm2 list
```

🚀 **Frontend setup successfully completed!** Next, we move to backend integration. 🎉
