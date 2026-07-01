# Java Fullstack Web Application Hosting using Docker

This repository demonstrates a **production‑style CI/CD pipeline** for a Java Fullstack Web Application. The project integrates **Maven, SonarQube, Nexus, Docker, Trivy, DockerHub, and Docker Swarm**, all orchestrated through **Jenkins Pipeline** with **SMTP Extended Email Notifications**.

---

## 📌 Project Overview
- **Backend:** Java (WAR packaged with Maven)
- **Frontend:** JSP/Servlets (deployed on Tomcat)
- **Database:** MySQL (accounts DB with user/role tables)
- **Deployment:** Docker Swarm stack with App + DB services
- **Pipeline:** Jenkins Declarative Pipeline

---

## 🔹 Tech Stack
- **Java + Maven** → Build & package WAR  
- **Apache Tomcat** → Application server  
- **MySQL 5.7** → Database backend  
- **SonarQube** → Static code analysis & quality gate enforcement  
- **Nexus Repository Manager** → Artifact storage (WAR files)  
- **Docker** → Containerization of App & DB  
- **Trivy** → Container image vulnerability scanning  
- **DockerHub** → Image registry  
- **Docker Swarm** → Multi‑service orchestration  
- **Jenkins** → CI/CD automation  
- **SMTP Extended Email Notification** → Email alerts on pipeline status  

---

## 🔹 CI/CD Pipeline Flow
The Jenkins pipeline automates the following stages:

1. **Source Code Checkout**  
   - Pulls code from GitHub repository.  

2. **Static Code Analysis (SonarQube)**  
   - Runs `mvn sonar:sonar` for code quality checks.  

3. **Quality Gate Validation**  
   - Enforces SonarQube rules with `waitForQualityGate`.  

4. **Build & Package Artifact**  
   - Compiles and packages WAR using Maven.  
   - Copies WAR into Docker app directory.  

5. **Upload Artifact to Nexus Repository**  
   - Stores WAR in Nexus for versioned artifact management.  

6. **Docker Image Build (App & DB)**  
   - Builds Docker images for application and database.  

7. **Container Image Security Scan (Trivy)**  
   - Scans images for vulnerabilities before pushing.  

8. **Push Docker Images to Registry**  
   - Publishes images to DockerHub.  

9. **Deploy Application Stack to Docker Swarm**  
   - Deploys services using `docker stack deploy`.  

10. **Post Actions (Notifications)**  
    - Sends email alerts via SMTP Extended Email Notification plugin.  
    - Emails include build number, status (SUCCESS/FAILURE), and duration.  
