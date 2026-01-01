# 🚀 Deploying a Next.js App on Ubuntu VPS

**Author:** Aditya Burse  

This guide shows a **real-world deployment flow** for a Next.js app on an Ubuntu VPS.  
Each step explains **what the command does and why it exists**, so beginners can truly understand deployment.

---

## ⭐ Step 1: Update the Server

```bash
sudo apt update && sudo apt upgrade -y
````

This tells Ubuntu to:

* Check for the latest package versions
* Update already installed software
* `-y` means **“yes to everything”**, so it doesn’t pause for confirmation

---

## ⭐ Step 2: Install Node.js (LTS)

```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
```

What this command does:

* Downloads a setup script from **NodeSource**
* Adds the official **LTS (Long Term Support)** Node.js repository to Ubuntu

Now install Node.js:

```bash
sudo apt install -y nodejs
```

This installs:

* **Node.js** → runs JavaScript on the server
* **npm** → installs project dependencies

Verify installation:

```bash
node -v
npm -v
```

---

## ⭐ Step 3: Install & Start Nginx

```bash
sudo apt install nginx
```

Installs **Nginx**, which acts as:

* A reverse proxy
* A traffic manager
* A security gate in front of your app

Start Nginx immediately:

```bash
sudo systemctl start nginx
```

Enable Nginx on server reboot:

```bash
sudo systemctl enable nginx
```

Check Nginx status:

```bash
sudo systemctl status nginx
```

---

## ⭐ Step 4: Move to Web Directory & Clone Project

```bash
cd /var/www/html
```

This is the standard directory where web applications usually live.

Clone your project:

```bash
git clone <your-repo-url>
```

Move into the project folder:

```bash
cd <project-name>
```

---

## ⭐ Step 5: Install Dependencies & Build the App

```bash
npm install
```

* Reads `package.json`
* Installs everything your Next.js app needs

Build the production version:

```bash
npm run build
```

* Creates an optimized production build
* Prepares the app to run efficiently on the server

---

## ⭐ Step 6: Install PM2 (App Bodyguard)

```bash
npm install -g pm2
```

PM2 is a process manager that:

* Keeps the app running
* Restarts it if it crashes
* Runs it in the background

Start the Next.js app using PM2:

```bash
pm2 start npm --name nextjs-app -- start
```

What PM2 does here:

* Runs `npm start`
* Names the process `nextjs-app`
* Keeps it alive **24/7**

Check status and logs:

```bash
pm2 status
pm2 logs
```

---

## ⭐ Step 7: Make the App Survive Server Reboot

```bash
pm2 startup
```

* Generates startup instructions for the system

Save current processes:

```bash
pm2 save
```

* Ensures PM2 restarts your app automatically after a reboot

---

## ⭐ Step 8: Configure Nginx as a Reverse Proxy

Open the Nginx config file:

```bash
sudo nano /etc/nginx/sites-available/default
```

Replace the content with:

```nginx
server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

### What this means (in simple words):

* Nginx listens on **port 80** (normal web traffic)
* When a request comes in:

  * It forwards the request to Next.js running on **port 3000**
* Users never see port `3000`
* Nginx handles everything publicly

Test and reload Nginx:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

---

## ✅ Final Result

* Users access the site via browser
* Nginx receives the request
* Next.js responds through PM2
* App stays online even after crashes or server reboot

---

### 💡 Beginner Tip

Don’t memorize commands.
Understand **why** each command exists — deployment becomes simple after that.

Happy Deploying! 🚀

```

Just tell me 👍
```
