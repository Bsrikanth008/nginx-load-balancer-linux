
# 🔀 Linux Load Balancer Project — Nginx

![Nginx](https://img.shields.io/badge/Nginx-1.24-009900?style=for-the-badge&logo=nginx&logoColor=white)
![RHEL](https://img.shields.io/badge/RHEL-Linux-EE0000?style=for-the-badge&logo=redhat&logoColor=white)
![Status](https://img.shields.io/badge/Status-Live-00cc44?style=for-the-badge)

> A production-grade Nginx Load Balancer on RHEL Linux distributing traffic across 3 backend servers.

## 📐 Architecture
\`\`\`
Client → Nginx (Port 80) → Server 1 (8081) - Dark Origin 🔴
                         → Server 2 (8082) - Ocean Deep 🔵
                         → Server 3 (8083) - Wild Earth 🟢
\`\`\`

## ✨ Features
- ⚡ Round Robin load balancing
- 🌐 3 backend servers with StreamFlix pages
- 🏥 Health checks & automatic failover
- 📊 Real-time status monitoring
- 🔥 Firewall configured

## 🛠️ Tech Stack
| Component | Technology |
|---|---|
| OS | RHEL / CentOS |
| Load Balancer | Nginx 1.24 |
| Backend | Python 3 HTTP Server |
| Algorithm | Round Robin |
| Frontend | HTML/CSS StreamFlix Theme |

## 🚀 Setup

### 1. Install Nginx
\`\`\`bash
sudo yum install nginx -y
sudo systemctl start nginx && sudo systemctl enable nginx
\`\`\`

### 2. Start Backend Servers
\`\`\`bash
cd /home/sree/servers/server1 && python3 -m http.server 8081 &
cd /home/sree/servers/server2 && python3 -m http.server 8082 &
cd /home/sree/servers/server3 && python3 -m http.server 8083 &
\`\`\`

### 3. Apply Config
\`\`\`bash
sudo cp load_balancer.conf /etc/nginx/conf.d/
sudo nginx -t && sudo systemctl reload nginx
\`\`\`

### 4. Open Firewall
\`\`\`bash
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload
\`\`\`

## ⚙️ Nginx Config
\`\`\`nginx
upstream backend_servers {
    server 127.0.0.1:8081;
    server 127.0.0.1:8082;
    server 127.0.0.1:8083;
}
server {
    listen 80;
    location / {
        proxy_pass http://backend_servers;
        add_header Cache-Control "no-cache";
    }
    location /status {
        stub_status on;
    }
    location /health {
        return 200 "Load Balancer OK\n";
    }
}
\`\`\`

## 🧪 Testing
\`\`\`bash
# Test Round Robin
for i in {1..6}; do curl -s http://localhost | grep "SERVER"; done

# Test health
curl http://localhost/health

# Monitor status
watch -n 2 'curl -s http://localhost/status'
\`\`\`

## 📊 Monitoring
\`\`\`bash
curl http://localhost/status
sudo tail -f /var/log/nginx/access.log
\`\`\`

## 👨‍💻 Author
**SrikanthBerla** — Linux Load Balancer Project | RHEL | March 2026
README

echo "README created!"
cat ~/nginx-loadbalancer-project/README.md
```

Then push to GitHub:
```bash
cd ~/nginx-loadbalancer-project
git add README.md
git commit -m "Add project README"
git push
```
