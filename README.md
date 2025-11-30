# DevSecOps Pipeline

This repository contains a **fully automated DevSecOps pipeline** designed for CI/CD environments.  
It integrates multiple security and quality tools to ensure robust, secure, and reliable software delivery.

## Features

- **Static Code Analysis:** SonarQube
- **Dependency Vulnerability Scanning:** Snyk, OWASP Dependency-Check
- **Python Security Checks:** Bandit
- **Container/File System Security Scans:** Trivy
- **Automated CI/CD Integration:** Jenkins pipeline
- **Automated Reporting:** HTML reports and Jenkins test results
- **Fail Build on Critical Vulnerabilities:** Optional enforcement for production-grade security

## Prerequisites

- Jenkins installed and configured
- SonarQube server connected to Jenkins
- Snyk account and token stored in Jenkins credentials
- Python environment for Bandit
- Trivy installed (for container or filesystem scans)
- OWASP Dependency-Check CLI installed

## Usage

1. **Clone the repository:**
```bash
git clone https://github.com/your-username/devsecops-pipeline.git
cd devsecops-pipeline
