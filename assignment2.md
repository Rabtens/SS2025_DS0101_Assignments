# CI/CD Pipeline Assignment Report

## Assignment Details

- **Course:** DSO101 - Continuous Integration and Continuous Deployment  
- **Program:** Bachelor's of Engineering in Software Engineering (SWE)  
- **Submission Date:** 28th May 2025  
- **Student:** [Kuenzang Rabten]  
- **Student ID:** [02230289]  

---

## Project Overview

This assignment demonstrates the implementation of a complete CI/CD pipeline using Jenkins for a Node.js to-do list application. The pipeline automates the entire software development lifecycle from code checkout to deployment.

---

## Table of Contents

- [CI/CD Pipeline Assignment Report](#cicd-pipeline-assignment-report)
  - [Assignment Details](#assignment-details)
  - [Project Overview](#project-overview)
  - [Table of Contents](#table-of-contents)
  - [Tools and Technologies Used](#tools-and-technologies-used)
  - [Pipeline Configuration](#pipeline-configuration)
    - [Pipeline Stages](#pipeline-stages)
  - [Implementation Steps](#implementation-steps)
    - [Step 1: Jenkins Setup](#step-1-jenkins-setup)
    - [Step 2: Plugin Installation](#step-2-plugin-installation)
    - [Step 3: Tool Configuration](#step-3-tool-configuration)
    - [Step 4: GitHub Repository Setup](#step-4-github-repository-setup)
    - [Step 5: `package.json` Configuration](#step-5-packagejson-configuration)
    - [Step 6: Testing Framework Setup](#step-6-testing-framework-setup)
    - [Step 7: Jenkinsfile Creation](#step-7-jenkinsfile-creation)
    - [Step 8: Pipeline Job Creation](#step-8-pipeline-job-creation)
  - [Challenges Faced](#challenges-faced)
    - [Technical Challenges](#technical-challenges)
    - [Configuration Challenges](#configuration-challenges)
  - [Results and Screenshots](#results-and-screenshots)
    - [Successful Pipeline Execution](#successful-pipeline-execution)
    - [Test Results](#test-results)
    - [Docker Deployment](#docker-deployment)
  - [](#)
  - [Lessons Learned](#lessons-learned)
    - [Technical Insights](#technical-insights)
    - [Best Practices Discovered](#best-practices-discovered)
    - [Process Improvements](#process-improvements)
  - [Future Enhancements](#future-enhancements)
    - [Possible Improvements](#possible-improvements)
    - [Monitoring and Alerts](#monitoring-and-alerts)
  - [Repository Links](#repository-links)
    - [GitHub Repository](#github-repository)
    - [Docker Hub](#docker-hub)
  - [Conclusion](#conclusion)
    - [Key Learnings](#key-learnings)
  - [Declaration](#declaration)

---

## Tools and Technologies Used

| Tool          | Purpose                        | Version       |
|---------------|--------------------------------|---------------|
| Jenkins       | CI/CD automation server        | Latest LTS    |
| GitHub        | Source code version control    | -             |
| Node.js       | JavaScript runtime environment | v20.x LTS     |
| npm           | Package manager                | Latest        |
| Jest          | JavaScript testing framework   | Latest        |
| Docker        | Application containerization   | Latest        |
| Docker Hub    | Container registry             | -             |

---

## Pipeline Configuration

### Pipeline Stages

The Jenkins pipeline consists of 5 main stages:

1. **Checkout Stage**  
   - Pulls the latest code from GitHub repository  
   - Uses the main branch as the source  

2. **Install Dependencies Stage**  
   - Runs `npm install` to install all project dependencies  
   - Downloads packages listed in `package.json`  

3. **Build Stage**  
   - Executes `npm run build` command  
   - Compiles the application for production  

4. **Test Stage**  
   - Runs unit tests using `npm test`  
   - Generates test reports in JUnit format  
   - Publishes test results to Jenkins  

5. **Deploy Stage**  
   - Builds Docker image of the application  
   - Pushes the image to Docker Hub registry  
   - Makes the application ready for deployment  

---

## Implementation Steps

### Step 1: Jenkins Setup
- Downloaded and installed Jenkins from [jenkins.io](https://www.jenkins.io)  
- Accessed Jenkins web interface at `localhost:8080`  
- Completed initial setup wizard  
- Created admin user account  

### Step 2: Plugin Installation
Installed the following Jenkins plugins:
- NodeJS Plugin
- Pipeline Plugin
- GitHub Integration Plugin
- Docker Pipeline Plugin

### Step 3: Tool Configuration
- Configured Node.js in Jenkins under **Manage Jenkins > Tools**
- Set up Node.js LTS v20.x with automatic npm installation
- Verified tool configuration was successful

### Step 4: GitHub Repository Setup
- Ensured Node.js application code was pushed to GitHub  
- Generated Personal Access Token (PAT) with:
  - `repo` access
  - `admin:repo_hook` permissions  
- Added GitHub credentials to Jenkins credential store

### Step 5: `package.json` Configuration
```json
{
  "scripts": {
    "test": "jest --ci --reporters=default --reporters=jest-junit",
    "build": "npm run build-script",
    "start": "node server.js"
  }
}
```
### Step 6: Testing Framework Setup

- Installed Jest: `npm install --save-dev jest`  
- Installed jest-junit: `npm install --save-dev jest-junit`  
- Created test files with proper test cases  

### Step 7: Jenkinsfile Creation

- Created Jenkinsfile with:  
  - Declarative pipeline syntax  
  - Error handling  
  - Post-build actions for test reporting  

### Step 8: Pipeline Job Creation

- Created new Pipeline job in Jenkins  
- Configured SCM to GitHub  
- Set up webhook for auto builds  
- Tested pipeline execution  

---

## Challenges Faced

### Technical Challenges

- **Node.js Plugin Configuration**  
  - *Problem*: npm not found  
  - *Solution*: Configured Node.js tool, updated PATH  

- **GitHub Authentication**  
  - *Problem*: Permission denied  
  - *Solution*: Used PAT with correct permissions  

- **Test Report Generation**  
  - *Problem*: Reports not visible  
  - *Solution*: Installed `jest-junit`, configured Jest  

- **Docker Integration**  
  - *Problem*: Docker commands failed  
  - *Solution*: Verified Docker installation and permissions  

### Configuration Challenges

- **Pipeline Syntax Errors**  
  - *Problem*: Syntax errors in Jenkinsfile  
  - *Solution*: Used syntax validator  

- **Build Script Issues**  
  - *Problem*: `npm run build` failed  
  - *Solution*: Added missing build script in `package.json`  

---

## Results and Screenshots

### Successful Pipeline Execution

![alt text](<assgn2_images/Screenshot from 2025-05-24 21-30-10.png>)

![alt text](<assgn2_images/Screenshot from 2025-05-24 21-49-23.png>)

![alt text](<assgn2_images/Screenshot from 2025-05-24 21-49-38.png>)

![alt text](<assgn2_images/Screenshot from 2025-05-24 22-06-13.png>)

![alt text](<assgn2_images/Screenshot from 2025-05-24 22-06-23.png>)

![alt text](<assgn2_images/Screenshot from 2025-05-26 20-50-30.png>)

![alt text](<assgn2_images/Screenshot from 2025-05-26 21-16-47.png>)

- All stages passed  
- Execution time: ~3–5 mins  
- All unit tests passed  

### Test Results

![alt text](<assgn2_images/Screenshot from 2025-05-26 21-17-10.png>)

- Unit tests ran successfully  
- JUnit reports generated  
- No failing tests  

### Docker Deployment

- Docker image built and pushed to Docker Hub  
- Image can be pulled and run anywhere  

![alt text](<assgn2_images/Screenshot from 2025-05-26 21-20-16.png>)
---

## Lessons Learned

### Technical Insights

- Importance of Jenkins tool configuration  
- Tool integration in a single pipeline  
- Docker usage in CI/CD  

### Best Practices Discovered

- Test components individually  
- Use error handling and post-build actions  
- Secure credentials in Jenkins  
- Document setup steps  

### Process Improvements

- Start automated testing early  
- Use version control for configs  
- Leverage logs and monitoring  

---

## Future Enhancements

### Possible Improvements

- Add code quality checks (ESLint, SonarQube)  
- Add security scanning  
- Deploy to staging before production  
- Enable auto rollback  
- Include performance testing  

### Monitoring and Alerts

- Email notifications on failure  
- Slack integration  
- Monitoring dashboards  

---

## Repository Links

### GitHub Repository

- **Main Repo**: [https://github.com/Rabtens/SS2025_DS0101_Assignments](https://github.com/yourusername/assignment1-node-app)  
- **Jenkinsfile**: Located in root directory  

### Docker Hub

- **Image**: [https://hub.docker.com/repository/docker/rabtens/node-app/tags/latest/sha256-7d43e9414cfba858b7e88c6b5fa212ca8ed844195fffbffc445592a586bd4577](https://hub.docker.com/r/yourusername/node-app)  
- **Tag**: `yourusername/node-app:latest`  

---

## Conclusion

This assignment successfully demonstrated a complete CI/CD pipeline using Jenkins. It automated the software lifecycle from code to deployment, ensuring consistent delivery.

### Key Learnings

- Jenkins configuration and CI/CD practices  
- Tool integration and workflow automation  
- Containerization and deployment strategies  

The pipeline is a solid foundation for future projects and can be extended further as needed.

---

## Declaration

I confirm that this work is my own and has been completed in accordance with the RUB Wheel of Academic Law. All sources and references have been properly acknowledged.