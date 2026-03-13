# 🚀 MASTER ENGINEERING & AI OPERATIONS PROTOCOL

```
=========================
ALWAYS LAST CONTROL
=========================
```

This document defines the **mandatory operating framework** for:

* Engineering work
* AI-assisted development
* Deployment operations
* Production protection
* System verification

The protocol ensures that all system changes are:

• Logical
• Safe
• Controlled
• Verifiable
• Reversible

**No step may be skipped.**

---

# 1. Mandatory Engineering Workflow

Every task must follow this exact sequence:

1. Investigation
2. Root Cause Analysis
3. End-to-End Fix Plan
4. Approval Gate
5. Implementation
6. Implementation Recap
7. Deployment Approval
8. Deployment
9. Human User Simulation Verification

Skipping steps is **not allowed**.

---

# 2. Investigation Phase

Before any change is made:

• Study the issue thoroughly
• Inspect logs and monitoring data
• Review database state
• Trace the code execution path
• Confirm the issue is reproducible

No fix should be attempted without **complete understanding of the problem**.

---

# 3. Root Cause Analysis

Identify the **actual root cause**, not the symptom.

Root cause documentation must include:

Problem
Root Cause
Affected Components
System Impact

Example:

```
Problem: Checkout fails when users attempt payment

Root Cause: Webhook signature verification mismatch

Affected Components:
payment-service
webhook-handler

Impact:
Users cannot complete payments
```

---

# 4. End-to-End Fix Plan

Before coding begins, a complete fix plan must be presented including:

• Root cause explanation
• Proposed solution
• Files to modify
• Affected systems
• Database impact
• UX impact
• Risks
• Rollback strategy

The plan must be **reviewed and approved before implementation begins**.

---

# 5. Approval Gate

Implementation may only begin when:

• The fix plan has been reviewed
• Explicit approval has been given

This prevents uncontrolled code changes.

---

# 6. Implementation Phase

After approval:

• Implement the solution
• Follow clean architecture principles
• Avoid shortcuts or temporary fixes

All changes must prioritize:

• Stability
• Maintainability
• Scalability
• User experience

---

# 7. Implementation Recap

After implementation is completed, provide a recap including:

Code Changes
Files modified or added

Logic Changes
Updated system behavior

Database Changes
Schema updates or migrations

Configuration Changes
Environment variables or configuration updates

Risk Notes
Potential side effects requiring monitoring

Deployment **must not occur before the recap is reviewed**.

---

# 8. Deployment Approval

Deployment may only occur **after recap approval**.

---

# 9. Deployment Strategy

Production deployments must ensure:

• Zero downtime
• Full system backup before deployment
• Zero user data loss
• Deployment verification

---

# 10. Approved Deployment Methods

Approved methods:

• rsync
• git pull on server
• tarball deployment

Deployment must guarantee:

• full file integrity
• build parity with local version
• rollback capability

---

# 11. Automated Server Control

Use **Paramiko** for:

• automated SSH authentication
• remote command execution
• deployment scripting
• automated verification

---

# 12. Secure Deployment Process

Deployment sequence:

1. Upload tarball segments
2. Reassemble archive on server
3. Extract files
4. Verify file integrity
5. Compare with local build output
6. Perform intelligent cleanup
7. Restart services if required

Goal:

```
100% deployment parity
zero file loss
```

---

# 13. Required Deployment Files

Every deployment must include the full application stack.

Backend

• API routes
• services
• middleware
• utilities

Frontend

• frontend source files
• compiled production build

Configuration

• next.config
• tailwind.config
• postcss.config
• environment templates
• build configuration files

Assets

• public directory
• images
• fonts
• static assets

Database Layer

• Prisma schema
• migrations
• Prisma client

---

# 14. Database Protection Rules

Database operations are **high-risk**.

The following command must **never run without explicit approval**:

```
prisma db push --force-reset
```

This command can destroy production data.

Safe migration method:

```
prisma migrate deploy
```

---

# 15. Human User Simulation (Mandatory)

After deployment, the system must be tested **exactly like a real user**.

Verification includes:

Visual Page Checks
Navigate pages and verify UI rendering.

Browser Console Inspection
Inspect:

• JavaScript errors
• network request failures
• runtime exceptions

Functional Testing
Verify:

• login
• dashboards
• forms
• payments
• admin functionality

Every page must be **fully error-free**.

---

# 16. Test Credentials

For deep verification retrieve credentials from:

```
C:\Users\chibu\Claude-Projects\Key\live keys.md
```

Test both:

• User account
• Admin account

---

# 17. Error Handling Policy

Generic errors are strictly prohibited.

Errors must always be:

• Specific
• Actionable
• Helpful
• Context-aware

Bad:

```
Something went wrong
```

Good:

```
Payment failed: Your card was declined by the issuing bank.

Please try another card or contact your bank.

Error Code: PAY-102
```

---

# 18. Database-Driven Error System

Error messages should be:

• stored in the database
• customizable by administrators
• dynamically rendered

Benefits:

• localization
• customizable messaging
• easier debugging

---

# 19. Anti-Hardcoding Policy

Hardcoding creates fragile systems.

Never hardcode:

• API URLs
• error messages
• feature flags
• roles or permissions
• environment values
• system limits
• file paths

Instead use:

• environment variables
• database configuration
• centralized config files
• admin settings
• feature flags

---

# 20. Build & Caching Policy

Every new build must generate **new content hashes** when files change.

Static hashed assets:

Cache duration

```
1 year
```

Non-hashed assets:

```
24–48 hours
```

The build system must:

• detect source changes
• regenerate bundles
• invalidate caches properly

---

# 21. AI Development Safety Rules

AI agents must never:

• invent APIs
• fabricate database fields
• guess environment variables
• assume system behavior

If uncertain, the AI must:

• inspect the code
• request clarification
• verify assumptions

---

# 22. Environment Isolation

Production must be isolated from development.

Required environments:

```
local
development
staging
production
```

Deployment flow:

```
Local → Development → Staging → Production
```

AI must **never deploy directly to production**.

---

# 23. Database Access Protection

AI systems must not have write access to production databases.

Architecture:

```
Primary Database (write)

       │

Read Replica (AI read-only)
```

---

# 24. Secrets Protection

Production secrets must never exist in source code.

Secrets must be stored in secure secret managers and injected at runtime.

---

# 25. Feature Flag Safety

All new features must deploy **disabled by default**.

Example:

```
feature_new_dashboard = false
feature_new_payment_flow = false
```

Features are enabled gradually after verification.

---

# 26. Versioned Release Deployment

Deployments must use versioned releases.

Example structure:

```
/var/www/app

/releases
/shared
/current
```

Active version:

```
current → /releases/release-003
```

The web server always serves from:

```
/var/www/app/current
```

---

# 27. Safe Deployment Flow

Deployment steps:

1. Upload new release
2. Extract to releases folder
3. Install dependencies
4. Build application
5. Run migrations safely
6. Verify build integrity
7. Switch symlink

```
current → new-release
```

Switch time: milliseconds.

Users experience **zero downtime**.

---

# 28. Instant Rollback

Rollback command:

```
ln -sfn /var/www/app/releases/previous-release /var/www/app/current
```

Rollback time:

```
5–10 seconds
```

---

# 29. Automated Health Checks

After deployment run:

```
GET /
GET /api/health
GET /login
GET /dashboard
```

If any fail:

```
automatic rollback
```

---

# 30. Database Backup Strategy

Before every deployment:

```
pg_dump database > backup.sql
```

Store backups with timestamps.

Example:

```
/backups
2026-03-13-predeploy.sql
```

---

# 31. Deployment Logging

Each deployment must generate a record:

Deployment ID
Timestamp
Commit Hash
Status
Rollback Availability

Logs stored in:

```
/deployments/logs
```

---

# 32. Emergency Kill Switch

If a critical failure occurs:

```
ENABLE_MAINTENANCE_MODE=true
```

The server redirects all requests to a maintenance page.

---

# 33. Final System Principles

All system changes must prioritize:

• reliability
• transparency
• maintainability
• user experience

The system must always remain:

• logical
• stable
• configurable
• scalable
• user-friendly

And must never include:

• generic errors
• hardcoded logic
• unsafe deployments

---

✅ **FINAL RESULT**

This protocol creates a system with:

• controlled engineering workflow
• safe AI-assisted development
• zero-downtime deployment
• instant rollback capability
• strong production protection
• predictable system behavior

This framework is suitable for **serious SaaS production environments** and scales safely with AI-assisted engineering.

---

# 34. 🛡️ The Absolute VPS Master Guide

Universal Edition • Drizzle ORM • PM2 Cluster • DDoS Protection • Complete Migration

## Prerequisites

Local Machine: Python 3 installed (pip install paramiko).  
Cloudflare: Required. Used to hide VPS IP and stop DDoS attacks.  
VPS: Ubuntu 20.04 or 22.04.

## Part 1: Domain DNS & Cloudflare

### Cloudflare Setup (DDoS Shield)

Change your domain's Nameservers to Cloudflare. This hides your real VPS IP.

```
# Cloudflare DNS Settings
Type: A     Name: @          Value: YOUR_VPS_IP    Status: Proxied (Orange Cloud) ✅
Type: A     Name: staging    Value: YOUR_VPS_IP    Status: DNS Only (Gray Cloud) ⚠️
Type: A     Name: monitor    Value: YOUR_VPS_IP    Status: DNS Only (Gray Cloud) ⚠️
```

## Part 2: Auto-Setup Script

```bash
#!/bin/bash
# 1. System Update & Utilities
sudo apt update && sudo apt upgrade -y
sudo apt install nginx git curl fail2ban apache2-utils -y

# 2. Install Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER

# 3. Setup Swap (Critical for Node/DB Memory)
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# 4. Setup Firewall
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw --force enable

# 5. Generate SSH Keys for GitHub
ssh-keygen -t ed25519 -C "server@vps" -f ~/.ssh/id_ed25519 -N ""
echo ">>> ADD THIS KEY TO GITHUB REPO SETTINGS -> DEPLOY KEYS <<<"
cat ~/.ssh/id_ed25519.pub

echo "Setup Complete. Log out and back in."
```

## Part 2.5: Nginx Performance & Security

### Main Config

Edit `/etc/nginx/nginx.conf`. Add these inside the `http {}` block.

```nginx
http {
    # ... existing settings ...

    # 1. GZIP COMPRESSION (Speed)
    gzip on;
    gzip_vary on;
    gzip_proxied any;
    gzip_comp_level 6;
    gzip_types text/plain text/css text/xml application/json application/javascript application/xml;

    # 2. RATE LIMITING (DDoS)
    # Limit requests to 10 per second per IP
    limit_req_zone $binary_remote_addr zone=mylimit:10m rate=10r/s;

    # 3. SECURITY HEADERS
    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";
}
```

### Site Config (Rate Limiting)

```nginx
server {
    listen 80;
    server_name example.com;

    location / {
        # Apply the rate limit
        limit_req zone=mylimit burst=20 nodelay;
        
        proxy_pass http://127.0.0.1:8001;
        
        # Browser Caching
        location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
            expires 1y;
        }
    }
}
```

## Part 3: Docker & Drizzle Setup (The Stack)

### Docker Compose

```yaml
services:
  web:
    build:
      context: .
      dockerfile: Dockerfile.prod
    restart: always
    ports:
      - "8001:8000"
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgres://app_user:strong_password@db:5432/app_db
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8000/health"]
      interval: 30s
      retries: 3
  db:
    image: postgres:15
    volumes:
      - ./postgres_data:/var/lib/postgresql/data
    environment:
      POSTGRES_DB: app_db
      POSTGRES_USER: app_user
      POSTGRES_PASSWORD: strong_password_here
    restart: always
```

### Dockerfile.prod (Drizzle + PM2)

Drizzle requires specific build steps. We use PM2 for clustering.

```dockerfile
# Dockerfile.prod
FROM node:18-alpine

WORKDIR /app

# Install PM2
RUN npm install -g pm2

# Install Dependencies
COPY package*.json ./
RUN npm install --production

# Copy Source
COPY . .

# Build Step (Adjust if using ts-node directly in prod)
RUN npm run build

# Start Command: Run Migrations THEN Start Server
# This ensures DB schema is updated before app starts
CMD ["sh", "-c", "npm run db:migrate && pm2-runtime ecosystem.config.js"]
```

### PM2 Ecosystem (Cluster Mode)

```javascript
// ecosystem.config.js
module.exports = {
  apps: [{
    name: "backend",
    script: "./dist/main.js", // Or your entry point
    instances: "2",           // Auto-scales to CPU cores
    exec_mode: "cluster",     // Load Balancing
    max_memory_restart: "1G", // Memory Safety
    env_production: {
      NODE_ENV: "production",
      PORT: 8000
    }
  }]
};
```

## Part 4: Live Migration Strategy

Moving an existing site? Follow this to keep data.

### Step 1: Backup Existing DB

```bash
# On OLD Server
pg_dump -U old_user -d old_db_name > backup_live.sql
```

### Step 2: Transfer & Restore

```bash
# 1. Transfer to NEW VPS
scp backup_live.sql user@YOUR_VPS_IP:/home/user/

# 2. On NEW VPS, start DB
docker-compose up -d db

# 3. Restore Data (Postgres)
cat /home/user/backup_live.sql | docker exec -i db_container_name psql -U app_user -d app_db
```

## Part 5: Tiered Backup Strategy

### Backup Script

Save as `backup_tiered.sh`. Keeps 4 hourly, 7 daily, 4 weekly, 3 monthly.

```bash
#!/bin/bash
CONTAINER_NAME="db_container_name"
DB_USER="app_user"
DB_NAME="app_db"
BACKUP_ROOT="/home/user/backups"
DATE=$(date +"%Y%m%d_%H%M%S")
DAY=$(date +"%Y%m%d")

mkdir -p $BACKUP_ROOT/temp
docker exec $CONTAINER_NAME pg_dump -U $DB_USER $DB_NAME > $BACKUP_ROOT/temp/backup_$DATE.sql

# HOURLY (Keep last 4)
mkdir -p $BACKUP_ROOT/hourly
cp $BACKUP_ROOT/temp/backup_$DATE.sql $BACKUP_ROOT/hourly/
ls -t $BACKUP_ROOT/hourly/*.sql | tail -n +5 | xargs rm -f

# DAILY (Keep last 7)
mkdir -p $BACKUP_ROOT/daily
if [ ! -f "$BACKUP_ROOT/daily/daily_$DAY.sql" ]; then
  cp $BACKUP_ROOT/temp/backup_$DATE.sql $BACKUP_ROOT/daily/daily_$DAY.sql
fi
ls -t $BACKUP_ROOT/daily/*.sql | tail -n +8 | xargs rm -f

# WEEKLY & MONTHLY logic...

rm $BACKUP_ROOT/temp/backup_$DATE.sql
```

### Cron Job

```bash
0 * * * * /var/www/production/backup_tiered.sh
```

## Part 6: Staging Environment

Staging runs on Port 8002 using a separate database.

```bash
# 1. Setup Folder
git clone git@github.com:username/repo.git /var/www/staging
cd /var/www/staging

# 2. Update docker-compose.yml for Staging
# Change ports: "8002:8000"
# Change DB Volume: ./postgres_data_staging:/var/lib/postgresql/data

# 3. Nginx Config (Password Protected)
server {
    listen 80;
    server_name staging.example.com;
    location / {
        auth_basic "Dev Only";
        auth_basic_user_file /etc/nginx/.htpasswd;
        proxy_pass http://127.0.0.1:8002;
    }
}
```

## Part 7: CI/CD Pipeline

```yaml
# .github/workflows/deploy.yml
name: Deploy
on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Deploy
      uses: appleboy/ssh-action@master
      with:
        host: ${{ secrets.HOST }}
        username: ${{ secrets.USER }}
        key: ${{ secrets.SSH_KEY }}
        script: |
          cd /var/www/production
          git pull origin main
          ./backup_tiered.sh
          # Drizzle migrate runs inside container on startup (see Dockerfile)
          docker-compose up -d --build
          sleep 10
          curl -f http://localhost:8000/health || exit 1
```

## Part 8: Remote Deployer (Paramiko)

Fixes fatal: could not read Username. Save as `deploy_controller.py`.

```python
import paramiko

HOST = "YOUR_VPS_IP"
USER = "root"
KEY_FILE = r"C:/Users/You/.ssh/id_rsa" 
PROJECT_PATH = "/var/www/production"
GIT_REPO_SSH = "git@github.com:username/repo.git" 

def main():
    client = paramiko.SSHClient()
    client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
    client.connect(HOST, username=USER, key_filename=KEY_FILE)
    
    # 1. Force Git SSH
    client.exec_command(f"cd {PROJECT_PATH} && git remote set-url origin {GIT_REPO_SSH}")
    
    # 2. Deploy
    stdin, stdout, stderr = client.exec_command(f"cd {PROJECT_PATH} && git pull && docker-compose up -d --build")
    print(stdout.read().decode())
    client.close()
```

## Part 9: Disaster Recovery

```bash
#!/bin/bash
# rollback.sh
docker-compose down
docker tag myapp_web:backup myapp_web:latest
docker-compose up -d
```

## Part 10: Free SSL

If using Cloudflare, set SSL Mode to "Full".

```bash
sudo certbot --nginx -d example.com -d staging.example.com
```

## Part 11: Monitoring & Security

### Fail2Ban (SSH Brute Force)

```bash
sudo bash -c 'cat > /etc/fail2ban/jail.local << EOF
[sshd]
enabled = true
maxretry = 3
bantime = 1h
EOF'
sudo systemctl restart fail2ban
```

### Uptime Kuma

```bash
docker run -d --restart=always -p 3001:3001 -v uptime-kuma:/app/data louislam/uptime-kuma:1

# Nginx Config for Monitor
# server { listen 80; server_name monitor.example.com; location / { proxy_pass http://127.0.0.1:3001; } }
```

## Part 12: Emergency Commands

```bash
# --- STATUS ---
docker ps
docker logs web_container --tail 100

# --- DATABASE RESTORE ---
cat /home/user/backups/daily/daily_20231027.sql | docker exec -i db_container_name psql -U app_user -d app_db

# --- PM2 INSIDE DOCKER ---
docker exec -it web_container_name pm2 monit
```

Universal Drizzle Edition.