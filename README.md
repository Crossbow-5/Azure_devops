# 🌐 End-to-End DevSecOps CI/CD Pipeline with Azure DevOps

Welcome to my DevOps portfolio project! This repository contains a complete, production-grade CI/CD pipeline built using **Azure DevOps**, designed to support secure and scalable deployments of a **Spring Boot** application across **Dev**, **Staging**, and **Production** environments.

---

## 🚀 Key Features

- ✅ Multi-environment deployment: Development, Staging, Production
- 🔐 Integrated **SAST** (SonarQube) and **DAST** (OWASP ZAP) security scanning
- 📦 Maven-based build pipeline with JFrog Artifactory publishing
- 🐳 Docker image creation, scanning (with Trivy), and push to Docker Hub & Azure ACR
- ☁️ Artifact uploads to **Azure Blob Storage** and **AWS S3**
- 🔄 Infrastructure automation using **Terraform-ready agents**
- 📈 Dynamic versioning and artifact tagging with `Build.BuildId`

---

## 🧰 Tools & Technologies Used

| Category       | Tools/Tech                     |
|----------------|-------------------------------|
| CI/CD          | Azure DevOps Pipelines         |
| Build Tool     | Maven                          |
| SCM            | GitHub                         |
| SAST           | SonarQube                      |
| DAST           | OWASP ZAP                      |
| Containerization| Docker                        |
| Container Registry | Azure Container Registry, Docker Hub |
| Artifact Management | JFrog Artifactory, Azure Blob, AWS S3 |
| IaC Ready Agent | Terraform                     |
| Security Scanning | Trivy (container image scanner) |
| Deployment     | Azure Container Instances (ACI), AWS EC2 (VM-based) |
| Monitoring     | Curl-based health check with HTTP response validation |

---

## 📁 Pipeline Structure

The YAML pipeline is structured into multiple stages:

1. **Agent & Tool Check**
   - Verifies presence of Terraform, Docker, Ansible, etc.

2. **SAST with SonarQube**
   - Static code analysis using Maven Sonar plugin.

3. **Java Build & Artifact Publishing**
   - Maven build, deploys to JFrog, uploads artifacts to Azure/AWS.

4. **Docker Build & Trivy Scan**
   - Builds Docker image, scans for vulnerabilities (LOW → CRITICAL).

5. **Push to ACR & Docker Hub**
   - Tags and pushes images to both registries.

6. **Deploy to ACI (Azure)**
   - Deploys Docker container in Azure for Dev testing.

7. **Deploy to Staging (AWS EC2)**
   - Stops running JAR, deploys new one, runs in background.

8. **Validate Staging**
   - Health check using HTTP status code.

9. **DAST Scan - Staging**
   - OWASP ZAP targeted scan and test result publishing.

10. **Deploy to Production (AWS EC2)**
    - Similar to staging deployment with additional validation.

11. **DAST Scan - Production**
    - Final OWASP ZAP scan on live production app.

---

## 📦 Artifact Naming Convention

- Java JAR: `ROOT$(Build.BuildId).jar`
- Docker Image Tags: `afrozmd/myapp:$(Build.BuildId)` and `devsecops_acr.azurecr.io/devsecops_acr:$(Build.BuildId)`

---

## ⚙️ Pipeline Trigger Rules

- **Triggered by branches**: `development`, `uat`, `production`
- **Excluded branches**: `master`, `feature*`, `releases/*`
- **File path exclusions**: `demofile-exclude.txt`, `megastar*`, `superstar-*`

---

## 🌍 Deployment URLs

| Environment | URL |
|-------------|-----|
| **Staging** | [http://staging.azureb46.xyz:8080/](http://staging.azureb46.xyz:8080/) |
| **Production** | [http://prod.azureb46.xyz:8080/](http://prod.azureb46.xyz:8080/) |

---

## 📄 Future Enhancements

- Add automated rollback on failed deployments
- Integrate Slack/MS Teams notifications
- Include Infrastructure provisioning (Terraform module integration)
- Add Helm + Kubernetes support for container orchestration
