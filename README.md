# 🛠️ Dummy Systemd Service - Beginner DevOps Project

## 🎯 Project Goal
This project helps you get hands-on experience with **Systemd** by creating a long-running background service in Linux. You'll learn how to:
- Write and run a custom background script
- Create a `systemd` service
- Enable auto-start on boot
- Log service output
- Monitor and manage service status

---

## 📋 Requirements
- A Linux server (tested on Ubuntu EC2)
- SSH access to the server
- `sudo` privileges

---

## 🧪 What the Service Does
- Runs a script called `dummy.sh`
- Appends `Dummy service is running...` to `/var/log/dummy-service.log` every **10 seconds**
- Auto-restarts if stopped or fails
- Auto-starts on system boot

---

## ⚙️ Step-by-Step Instructions

### ✅ 1. Create the Script

```bash
sudo nano /usr/local/bin/dummy.sh
Paste the following code:

bash
Copy
Edit
#!/bin/bash

while true; do
  echo "Dummy service is running..." >> /var/log/dummy-service.log
  sleep 10
done
Make it executable:

bash
Copy
Edit
sudo chmod +x /usr/local/bin/dummy.sh
✅ 2. Create the systemd Service
bash
Copy
Edit
sudo nano /etc/systemd/system/dummy.service
Paste this content:

ini
Copy
Edit
[Unit]
Description=Dummy Long-Running Service
After=network.target

[Service]
ExecStart=/usr/local/bin/dummy.sh
Restart=always
RestartSec=5
StandardOutput=append:/var/log/dummy-service.log
StandardError=append:/var/log/dummy-service.log

[Install]
WantedBy=multi-user.target
✅ 3. Reload systemd & Start the Service
bash
Copy
Edit
sudo systemctl daemon-reload
sudo systemctl start dummy
sudo systemctl enable dummy
✅ 4. Monitor the Service
🔎 Check status:
bash
Copy
Edit
sudo systemctl status dummy
📄 Follow log output:
bash
Copy
Edit
sudo tail -f /var/log/dummy-service.log
🛑 Stop the service:
bash
Copy
Edit
sudo systemctl stop dummy
❌ Disable it from auto-starting:
bash
Copy
Edit
sudo systemctl disable dummy
📁 Recommended Repo Structure
Copy
Edit
dummy-systemd-service/
├── dummy.sh
├── dummy.service
├── README.md
