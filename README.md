# TravelMemory - Full Stack Deployment (MERN Stack)

This project demonstrates the end-to-end deployment of the **TravelMemory** MERN stack application on an AWS EC2 instance, including domain mapping, load balancing, and reverse proxy setup.

---

##  Project Overview

- **Frontend**: React.js  
- **Backend**: Node.js + Express  
- **Database**: MongoDB  
- **Deployment**: Amazon EC2 (Ubuntu)  
- **Load Balancing**: AWS EC2 + Cloudflare + NGINX  
- **Domain Management**: Cloudflare (with custom domain)

---

##  Features Implemented

- Backend setup with Node.js and Express (Port `3000`)
- Frontend setup with React.js (Port `3001`)
- Configured NGINX as a reverse proxy
- Connected front-end with back-end using environment variables
- Deployed both services on EC2
- Configured multiple instances for scaling
- Created an AWS Application Load Balancer
- Connected custom domain using Cloudflare
- SSL (HTTPS) via Certbot (To be implemented or rate-limited currently)
- Complete documentation and architecture diagram

---

##  How to Deploy (Steps Summary)

### 1. Clone the Repository

```bash
git clone https://github.com/RahulKagra/TravelMemory/tree/main/backend
```

### 2.Backend Setup
```bash
cd backend
npm install
# Create and configure your .env file
# Example .env:
# MONGODB_URL=mongodb+srv://rahulkagra1625:Za7kWRTJUsQ0Pg6c@rahulkagra-cluster1.fr84c6p.mongodb.net/
# PORT=3000
node index.js
```
###3. Frontend Setup
```bash
cd frontend
npm install
npm start
```
### 4. NGINX Configuration
Set up a reverse proxy on your EC2 instance to:
```bash
server {
    listen 80;

    server_name rahul1625;

    location /api/ {
        proxy_pass http://localhost:3000/;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    location / {
        proxy_pass http://localhost:8000/;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```
### 5.Load Balancer + Scaling
    Create multiple EC2 instances running the app

    Add them under an AWS Application Load Balancer

    Update Cloudflare to point to the load balancer
### 6.Cloudflare + Domain
    Add domain to Cloudflare

    Create a CNAME record pointing to the AWS Load Balancer DNS

    Create an A record pointing to your EC2 instance

    Use Certbot for HTTPS setup
## Live URL
http://rahulkagra.it.com







    






