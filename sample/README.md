Here is the **clear and detailed version (v2.0)** of your **Linux Admin Levels (Basic → Intermediate → Advanced)** with short explanations + examples.
This is perfect for **DevOps interview, learning, or job tasks**.

---

# ⭐ **Linux Admin Skill Levels – Full Explanation (Version 2.0)**

---

# **LEVEL 1 – BASIC (FOUNDATIONAL SKILLS)**

These are the essential tasks every DevOps/Linux engineer must know.

## 1️⃣ **Set up users, groups for dev team**

Create user:

```bash
sudo useradd devuser
sudo passwd devuser
```

Create group:

```bash
sudo groupadd developers
```

Add user to group:

```bash
sudo usermod -aG developers devuser
```

---

## 2️⃣ **Manage permissions for project directories**

Set directory owner:

```bash
sudo chown devuser:developers /opt/app
```

Set permissions:

```bash
sudo chmod 770 /opt/app
```

Give only group access:

```bash
sudo chmod -R g+rw /opt/app
```

---

## 3️⃣ **Install required packages (git, nginx, java)**

```bash
sudo apt install git nginx openjdk-11-jdk -y
```

Check versions:

```bash
git --version
nginx -v
java -version
```

---

## 4️⃣ **Check system info (memory, CPU, disks)**

Check memory:

```bash
free -h
```

Check CPU:

```bash
lscpu
```

Check disks:

```bash
df -h
```

Check processes:

```bash
top
```

---

# **LEVEL 2 – INTERMEDIATE (DAILY DEVOPS TASKS)**

## 5️⃣ **Automate backups with Cron**

Open cron:

```bash
crontab -e
```

Example backup job (daily at 2AM):

```
0 2 * * * tar -czf /backup/app-$(date +\%F).tar.gz /opt/app
```

---

## 6️⃣ **Create shell scripts: log cleanup, service restart, health checks**

### Log cleanup script

```bash
#!/bin/bash
find /var/log -type f -mtime +10 -delete
```

### Service restart script

```bash
#!/bin/bash
sudo systemctl restart nginx
```

### Health check script

```bash
#!/bin/bash
curl -I http://localhost:80
```

Make executable:

```bash
chmod +x script.sh
```

---

## 7️⃣ **Manage logs under /var/log**

List logs:

```bash
ls -l /var/log
```

Check syslog:

```bash
tail -f /var/log/syslog
```

Check nginx logs:

```bash
tail -f /var/log/nginx/access.log
```

---

## 8️⃣ **Monitor system performance & troubleshoot services**

Check CPU/memory usage:

```bash
htop
```

Check service status:

```bash
systemctl status nginx
```

Find which process uses most memory:

```bash
ps aux --sort=-%mem | head
```

---

# **LEVEL 3 – ADVANCED (PRODUCTION-READY LINUX ADMIN)**

## 9️⃣ **Create custom systemd service for your application**

Create file:

```bash
sudo nano /etc/systemd/system/myapp.service
```

Add:

```
[Unit]
Description=My Application Service
After=network.target

[Service]
ExecStart=/usr/bin/java -jar /opt/app/app.jar
Restart=always

[Install]
WantedBy=multi-user.target
```

Enable service:

```bash
sudo systemctl enable myapp
sudo systemctl start myapp
```

---

## 🔟 **SSH hardening for security**

Disable root login:

```bash
sudo nano /etc/ssh/sshd_config
```

Set:

```
PermitRootLogin no
PasswordAuthentication no
```

Restart:

```bash
sudo systemctl restart sshd
```

---

## 1️⃣1️⃣ **LVM setup for storage scaling**

Create physical volume:

```bash
sudo pvcreate /dev/sdb
```

Create volume group:

```bash
sudo vgcreate myvg /dev/sdb
```

Create logical volume:

```bash
sudo lvcreate -L 10G -n mylv myvg
```

Format:

```bash
mkfs.ext4 /dev/myvg/mylv
```

Mount:

```bash
mount /dev/myvg/mylv /mnt/data
```

---

## 1️⃣2️⃣ **Configure firewall rules**

Allow SSH:

```bash
sudo ufw allow 22
```

Allow HTTP:

```bash
sudo ufw allow 80
```

Enable firewall:

```bash
sudo ufw enable
```

---

## 1️⃣3️⃣ **Implement logrotate for app logs**

Create rule:

```bash
sudo nano /etc/logrotate.d/myapp
```

Add:

```
/var/log/myapp/*.log {
    weekly
    rotate 4
    compress
    missingok
    notifempty
}
```

Test logrotate:

```bash
sudo logrotate -d /etc/logrotate.conf
```

---

# 🎯 **DONE! This is the clean, clear Version 2.0**
