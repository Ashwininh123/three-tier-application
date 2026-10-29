# 🏗️ AWS 3-Tier Web Application

<p align="center">

### Production-Style Full-Stack Application Deployed on AWS

**React • Node.js • Nginx • Amazon EC2 • Application Load Balancer • Auto Scaling • Aurora/MySQL**

</p>

<p align="center">

![AWS](https://img.shields.io/badge/AWS-Cloud-232F3E?logo=amazonaws&logoColor=white)
![EC2](https://img.shields.io/badge/Amazon%20EC2-Compute-FF9900?logo=amazonec2&logoColor=white)
![React](https://img.shields.io/badge/React-Frontend-61DAFB?logo=react&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-Backend-339933?logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express.js-API-000000?logo=express&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-Web%20Server-009639?logo=nginx&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-Database-4479A1?logo=mysql&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-Repository-181717?logo=github&logoColor=white)

</p>

---

# 📑 Table of Contents

- 🎯 [Overview](#-overview)
- 🎯 [Objectives](#-objectives)
- 🏗️ [Architecture](#️-architecture)
- ⚡ [Application Flow](#-application-flow)
- ☁️ [AWS Services](#️-aws-services)
- 🌐 [Web Tier](#-web-tier)
- ⚙️ [Application Tier](#️-application-tier)
- 🗄️ [Database Tier](#️-database-tier)
- 🔐 [Security & Networking](#-security--networking)
- 📈 [Scalability & Availability](#-scalability--availability)
- 🚀 [Application Features](#-application-features)
- 🧰 [Tech Stack](#-tech-stack)
- 📁 [Project Structure](#-project-structure)
- 🔄 [Deployment Workflow](#-deployment-workflow)
- 🧠 [Key Engineering Concepts](#-key-engineering-concepts)
- 📚 [What I Learned](#-what-i-learned)
- 🚀 [Future Improvements](#-future-improvements)
- ⚡ [Quick Start](#-quick-start)
- 👩‍💻 [Author](#-author)

---

# 🎯 Overview

The **AWS 3-Tier Web Application** is a full-stack cloud project designed to demonstrate how a web application can be deployed using a structured three-tier architecture on AWS.

The application separates the system into three independent layers:

- 🌐 **Web Tier** — React frontend served through Nginx on Amazon EC2.
- ⚙️ **Application Tier** — Node.js/Express backend running on Amazon EC2 behind an Application Load Balancer.
- 🗄️ **Database Tier** — Aurora/MySQL-compatible database for persistent application data.

This separation provides a clear architecture for managing application traffic, business logic, and persistent data independently.

---

# 🎯 Objectives

The main objectives of this project were:

- 🌐 Understand AWS 3-tier architecture.
- 🧩 Separate frontend, backend, and database layers.
- ⚛️ Deploy a React application on Amazon EC2.
- 🌐 Configure Nginx as a web server.
- ⚙️ Deploy a Node.js/Express backend.
- ⚖️ Use an Application Load Balancer for backend traffic.
- 📈 Understand EC2 Auto Scaling.
- 🗄️ Connect the backend with an Aurora/MySQL-compatible database.
- 🔐 Understand AWS networking and security.
- ☁️ Build a production-style cloud deployment.
- 🔄 Learn how different AWS components communicate with each other.

---

# 🏗️ Architecture

The project follows a standard three-tier architecture.

```text
                         INTERNET
                            |
                            v
                  +-------------------+
                  |     WEB TIER      |
                  |                   |
                  |    Amazon EC2     |
                  |      Nginx        |
                  |   React Frontend  |
                  +---------+---------+
                            |
                            | HTTP / API
                            v
                  +-------------------+
                  | APPLICATION TIER  |
                  |                   |
                  | Application Load  |
                  |     Balancer      |
                  |        |          |
                  |     Node.js       |
                  |     Express       |
                  |       EC2         |
                  +---------+---------+
                            |
                            | SQL
                            v
                  +-------------------+
                  |   DATABASE TIER   |
                  |                   |
                  |   Aurora / MySQL  |
                  |                   |
                  |  Persistent Data  |
                  +-------------------+
```

## Three Independent Layers

| Layer | Main Responsibility | Technologies |
|---|---|---|
| 🌐 Web Tier | Serves frontend | React, Nginx, Amazon EC2 |
| ⚙️ Application Tier | Handles business logic and APIs | Node.js, Express, EC2, ALB |
| 🗄️ Database Tier | Stores persistent data | Aurora / MySQL |

This separation improves:

- Maintainability
- Scalability
- Security
- Troubleshooting
- Separation of responsibilities

---

# ⚡ Application Flow

The complete request flow is:

```text
                         USER
                           |
                           v
                    React Frontend
                           |
                           v
                         Nginx
                           |
                           | API Request
                           v
              Application Load Balancer
                           |
                           v
                  Node.js / Express
                           |
                           | SQL Query
                           v
                     Aurora / MySQL
                           |
                           | Database Response
                           v
                  Node.js / Express
                           |
                           | API Response
                           v
                    React Frontend
                           |
                           v
                         USER
```

## Step-by-Step Flow

1. The user opens the web application.
2. The request reaches the Web Tier.
3. Nginx serves the React frontend.
4. React sends an API request to the backend.
5. The request reaches the Application Load Balancer.
6. The ALB forwards the request to a backend EC2 instance.
7. Node.js/Express processes the request.
8. The backend communicates with Aurora/MySQL.
9. The database processes the SQL query.
10. The database returns the requested information.
11. Node.js/Express sends the API response.
12. React updates the user interface.

---

# ☁️ AWS Services

| AWS Service | Purpose |
|---|---|
| **Amazon EC2** | Hosts frontend and backend components |
| **Application Load Balancer** | Distributes backend application traffic |
| **EC2 Auto Scaling** | Supports horizontal scaling of backend instances |
| **Amazon Aurora / MySQL** | Stores persistent application data |
| **Amazon VPC** | Provides isolated cloud networking |
| **Security Groups** | Controls network traffic |
| **IAM** | Provides access and permission management |

---

# 🌐 Web Tier

The Web Tier is responsible for serving the frontend application.

## Components

- Amazon EC2
- Nginx
- React

## Responsibilities

- Host the frontend application.
- Serve React static files.
- Handle incoming web traffic.
- Provide the user interface.
- Send API requests toward the Application Tier.

## Web Tier Flow

```text
             USER
               |
               v
          Amazon EC2
               |
               v
             Nginx
               |
               v
        React Frontend
```

Nginx acts as the web server responsible for serving the built React application.

---

# ⚙️ Application Tier

The Application Tier contains the backend business logic of the application.

## Components

- Node.js
- Express.js
- Amazon EC2
- Application Load Balancer

## Responsibilities

- Receive API requests.
- Process application logic.
- Validate requests.
- Handle transaction operations.
- Communicate with the database.
- Return API responses.

## Application Flow

```text
React
  |
  v
Application Load Balancer
  |
  v
Node.js
  |
  v
Express.js
  |
  v
Aurora / MySQL
```

The Application Load Balancer provides a controlled entry point for backend traffic and can distribute requests across backend EC2 instances.

---

# 🗄️ Database Tier

The Database Tier stores the application's persistent data.

## Database

**Amazon Aurora / MySQL-compatible database**

## Responsibilities

- Store transactions.
- Retrieve transactions.
- Insert records.
- Update records.
- Delete records.
- Maintain persistent application data.

## Database Flow

```text
Node.js / Express
       |
       | SQL
       v
Aurora / MySQL
       |
       v
Persistent Data
```

The database layer is kept separate from the Web and Application layers.

---

# 🔐 Security & Networking

Security is a key part of the three-tier architecture.

The architecture is designed so that each layer communicates only with the layer it requires.

```text
Internet
   |
   v
Web Tier
   |
   v
Application Tier
   |
   v
Database Tier
```

## Security Groups

Security Groups can be configured to control communication between the different layers.

| Layer | Allowed Traffic |
|---|---|
| 🌐 Web Tier | HTTP / HTTPS |
| ⚙️ Application Tier | API traffic from Web Tier |
| 🗄️ Database Tier | MySQL traffic from Application Tier |

## Security Principles

- 🔐 Network isolation
- 🛡️ Controlled inbound traffic
- 🔒 Restricted database access
- 🌐 Internal application communication
- 👤 Least-privilege access
- 🧩 Separation of responsibilities

---

# 📈 Scalability & Availability

The Application Tier is designed to support horizontal scaling.

The Application Load Balancer can distribute traffic across multiple backend EC2 instances.

```text
                 Application Load Balancer
                          |
             +------------+------------+
             |            |            |
             v            v            v
           EC2 #1       EC2 #2       EC2 #3
          Node.js      Node.js      Node.js
```

## Horizontal Scaling

Instead of depending on a single backend server, additional instances can be introduced as workload increases.

```text
Low Traffic
    |
    v
  EC2 #1


Higher Traffic
    |
    v
EC2 #1 + EC2 #2


High Traffic
    |
    v
EC2 #1 + EC2 #2 + EC2 #3
```

## Benefits

- ⚖️ Traffic distribution
- 📈 Horizontal scaling
- 🛡️ Better application resilience
- 🔄 Reduced dependency on a single backend instance
- 🚀 Support for increasing workloads

---

# 🚀 Application Features

The application provides a simple transaction-management interface.

## Features

- ➕ Add transactions
- 👀 View transactions
- 🗑️ Delete transactions
- 🔄 Fetch transaction data
- 💾 Store data in MySQL-compatible database
- 🖥️ React-based interface
- 🔌 REST API communication

## Feature Flow

```text
User Interface
      |
      v
React
      |
      v
REST API
      |
      v
Node.js / Express
      |
      v
Aurora / MySQL
```

---

# 🧰 Tech Stack

## ☁️ Cloud & Infrastructure

| Category | Technology |
|---|---|
| Cloud Platform | AWS |
| Compute | Amazon EC2 |
| Load Balancing | Application Load Balancer |
| Scaling | EC2 Auto Scaling |
| Networking | Amazon VPC |
| Security | Security Groups, IAM |
| Database | Amazon Aurora / MySQL |

## 🎨 Frontend

```text
React
JavaScript
HTML
CSS
```

## ⚙️ Backend

```text
Node.js
Express.js
REST APIs
```

## 🌐 Web Server

```text
Nginx
```

## 🗄️ Database

```text
Amazon Aurora
MySQL
SQL
```

## 🛠️ Development Tools

```text
Git
GitHub
VS Code
npm
Linux
```

---

# 📁 Project Structure

```text
3-tier-architecture-app/
│
├── application-code/
│   │
│   ├── frontend/
│   │   ├── public/
│   │   ├── src/
│   │   ├── package.json
│   │   └── ...
│   │
│   └── backend/
│       ├── routes/
│       ├── controllers/
│       ├── models/
│       ├── config/
│       ├── server.js
│       └── package.json
│
├── 3 Tier Architecture.png
│
├── Documentation.txt
│
├── .gitignore
│
└── README.md
```

---

# 🔄 Deployment Workflow

The application follows a layered deployment process.

```text
                         DEVELOPER
                             |
                             v
                    GitHub Repository
                             |
                 +-----------+-----------+
                 |                       |
                 v                       v
        Frontend Application     Backend Application
                 |                       |
                 v                       v
            Amazon EC2              Amazon EC2
                 |                       |
                 v                       v
               Nginx                  Node.js
                                         |
                                         v
                               Application Load
                                   Balancer
                                         |
                                         v
                               Backend EC2 Instances
                                         |
                 +-----------------------+
                 |
                 v
             Aurora / MySQL
```

## Deployment Stages

```text
Developer
    |
    v
GitHub
    |
    +---------------------+
    |                     |
    v                     v
Frontend               Backend
    |                     |
    v                     v
EC2 + Nginx          EC2 + Node.js
                          |
                          v
                    Application Load
                       Balancer
                          |
                          v
                    Auto Scaling
                          |
                          v
                    Aurora / MySQL
```

---

# 🧠 Key Engineering Concepts

This project demonstrates several important cloud engineering concepts.

## 1. Three-Tier Architecture

The application is divided into:

```text
Web Tier
    ↓
Presentation Layer


Application Tier
    ↓
Business Logic


Database Tier
    ↓
Persistent Data
```

Each layer has a clearly defined responsibility.

## 2. Load Balancing

The Application Load Balancer provides a centralized entry point for backend traffic and distributes requests across available backend instances.

## 3. Horizontal Scaling

Multiple EC2 instances can be used to handle increasing application traffic.

## 4. Separation of Concerns

The frontend, backend, and database are independently managed.

## 5. Network Isolation

Different components can be placed into controlled network paths using VPCs and Security Groups.

## 6. Stateless Application Design

The backend can be replicated across multiple EC2 instances while persistent application data remains in the database layer.

## 7. Cloud Architecture

The project demonstrates how compute, networking, load balancing, scaling, application services, and databases work together in AWS.

---

# 📚 What I Learned

Through this project, I gained practical understanding of:

- ☁️ AWS cloud architecture
- 🏗️ Three-tier application design
- 🖥️ Amazon EC2 deployment
- 🌐 Nginx configuration
- ⚙️ Node.js backend deployment
- 🔌 REST API communication
- ⚖️ Application Load Balancing
- 📈 EC2 Auto Scaling
- 🗄️ MySQL-compatible databases
- 🔐 Security Groups
- 🌐 VPC networking
- 👤 IAM concepts
- 🐧 Linux server management
- 🔄 Application deployment
- 🛠️ Cloud troubleshooting

---

# 🚀 Future Improvements

The project can be extended with additional production-oriented capabilities.

- 🔒 HTTPS using AWS Certificate Manager
- 🌐 Route 53 custom domain
- 🔐 AWS Secrets Manager for database credentials
- 📊 Amazon CloudWatch monitoring and logging
- 🔄 CI/CD using GitHub Actions
- 🐳 Docker-based deployment
- 🧱 Infrastructure as Code using Terraform
- 🚀 AWS ECS / Fargate deployment
- 🗄️ Aurora Multi-AZ configuration
- 🛡️ AWS WAF integration
- 📈 Advanced monitoring and alerting
- 🔑 IAM role-based access instead of static credentials

---

# ⚡ Quick Start

## 1. Clone the Repository

```bash
git clone https://github.com/niharikaSinghh/3-tier-architecture-app.git
```

```bash
cd 3-tier-architecture-app
```

---

## 2. Frontend Setup

Navigate to the frontend directory:

```bash
cd application-code/frontend
```

Install dependencies:

```bash
npm install
```

Start the development server:

```bash
npm start
```

---

## 3. Backend Setup

Open another terminal and navigate to the backend:

```bash
cd application-code/backend
```

Install dependencies:

```bash
npm install
```

Start the backend:

```bash
node server.js
```

---

## 4. Configure Database

Configure the database connection using environment variables.

Example:

```env
DB_HOST=your-database-endpoint
DB_USER=your-database-user
DB_PASSWORD=your-database-password
DB_NAME=your-database-name
DB_PORT=3306
```

> **Never commit database passwords, AWS access keys, or other secrets to GitHub.**

---

## 5. AWS Deployment

The cloud deployment follows this architecture:

### Frontend

```text
React
   ↓
Amazon EC2
   ↓
Nginx
```

### Backend

```text
Node.js
   ↓
Amazon EC2
   ↓
Application Load Balancer
   ↓
EC2 Auto Scaling
```

### Database

```text
Application Tier
   ↓
Aurora / MySQL
```

---

# 📊 Project Highlights

| Area | Implementation |
|---|---|
| Architecture | AWS 3-Tier |
| Frontend | React |
| Web Server | Nginx |
| Backend | Node.js + Express |
| Compute | Amazon EC2 |
| Load Balancing | Application Load Balancer |
| Scaling | EC2 Auto Scaling |
| Database | Aurora / MySQL |
| Networking | Amazon VPC |
| Security | Security Groups + IAM |
| Version Control | Git + GitHub |

---

# 💡 Key Takeaway

The main goal of this project was not simply to deploy a website.

It was to understand how a complete cloud application can be structured into independent layers.

```text
                 ┌─────────────────────┐
                 │        USERS        │
                 └──────────┬──────────┘
                            |
                            v
                 ┌─────────────────────┐
                 │      WEB TIER       │
                 │    EC2 + Nginx      │
                 │       React         │
                 └──────────┬──────────┘
                            |
                            v
                 ┌─────────────────────┐
                 │  APPLICATION TIER   │
                 │   ALB + EC2         │
                 │ Node.js + Express   │
                 └──────────┬──────────┘
                            |
                            v
                 ┌─────────────────────┐
                 │    DATABASE TIER    │
                 │   Aurora / MySQL    │
                 └─────────────────────┘
```

The architecture separates:

**Presentation → Business Logic → Persistent Data**

This makes the application easier to maintain, scale, secure, and troubleshoot.

---

# 👩‍💻 Author

## Niharika Singh

**B.Tech Computer Science Engineering | Cloud & Data Analytics**

### Areas of Interest

- ☁️ AWS Cloud Engineering
- 📊 Data Analytics
- 🐍 Python
- 🗄️ SQL
- 📈 Power BI
- 🏗️ Cloud Architecture
- 🚀 DevOps & Automation

### 🔗 Connect

- 💻 GitHub: [github.com/niharikaSinghh](https://github.com/niharikaSinghh)
- 💼 LinkedIn: [Connect on LinkedIn](https://www.linkedin.com/)

---

<p align="center">

### ⭐ If you found this project useful, consider giving it a star!

</p>

<p align="center">

**Built with ☁️ AWS • ⚛️ React • 🟢 Node.js • 🌐 Nginx • 🗄️ MySQL**
Testing Jenkins CI/CD webhook
</p>
