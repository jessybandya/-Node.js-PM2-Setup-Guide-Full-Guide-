# 🚀 Node.js + PM2 Setup Guide (Full Guide)

This guide covers:

* Installing Node.js without sudo (using NVM)
* Setting up your project
* Creating a test route
* Running and managing your app with PM2

---

## 🔧 0. Install Node.js (No `sudo` Required)

### 1. Install NVM

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

If curl fails:

```bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

---

### 2. Activate NVM

```bash
source ~/.bashrc
```

If that doesn’t work:

```bash
source ~/.profile
```

---

### 3. Install Node.js

```bash
nvm install 18
nvm use 18
```

---

### 4. Verify Installation

```bash
node -v
npm -v
```

---

### 5. Install PM2

```bash
npm install -g pm2
```

Check:

```bash
pm2 -v
```

---

## 📁 1. Create Project Directory

```bash
mkdir my-node-app
cd my-node-app
```

---

## 📦 2. Initialize Project

```bash
npm init -y
```

---

## 📝 3. Create Dummy App

```bash
nano app.js
```

Paste:

```javascript
const http = require('http');

const PORT = 5000;

const server = http.createServer((req, res) => {
    if (req.url === '/test') {
        res.writeHead(200, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ message: 'Test route is working 🚀' }));
    } else {
        res.writeHead(404, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ error: 'Route not found' }));
    }
});

server.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

Save and exit:

```
CTRL + X → Y → ENTER
```

---

## ▶️ 4. Test App

```bash
node app.js
```

Visit:

```
http://your-server-ip:5000/test
```

---

## ⚡ 5. Run with PM2

```bash
pm2 start app.js --name my-app
```

---

## 📊 6. PM2 Commands

### List apps

```bash
pm2 list
```

### Monitor

```bash
pm2 monit
```

### Logs

```bash
pm2 logs my-app
```

---

## 🔄 7. Manage App

```bash
pm2 restart my-app
pm2 stop my-app
pm2 delete my-app
```

---

## ⏸️ 8. Pause / Resume

```bash
pm2 stop my-app     # pause
pm2 restart my-app  # resume
```

---

## 💾 9. Save Processes

```bash
pm2 save
```

---

## 🔁 10. Auto Start on Reboot

```bash
pm2 startup
```

Then run the command it outputs.

---

## 📁 11. Project Structure

```
my-node-app/
│
├── app.js
├── package.json
└── node_modules/
```

---

## ⚙️ 12. Useful Tips

### Use environment port (important for hosting)

```javascript
const PORT = process.env.PORT || 3000;
```

---

### Restart all apps

```bash
pm2 restart all
```

---

### Stop all apps

```bash
pm2 stop all
```

---

## 🚨 Common Issues

### App not accessible

* Port blocked by hosting provider
* Firewall restrictions
* Use reverse proxy (Apache/Nginx)

---

## 🎯 Final Workflow

```bash
mkdir my-node-app
cd my-node-app
npm init -y
nano app.js
node app.js
pm2 start app.js --name my-app
pm2 save
```

---

## ✅ Done

Your Node.js app is now:

* Running in the background
* Managed with PM2
* Ready for deployment 🚀
