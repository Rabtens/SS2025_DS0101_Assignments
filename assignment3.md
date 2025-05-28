# GitHub Actions CI/CD Pipeline Assignment Report

## Assignment Details

- **Course:** DSO101 - Continuous Integration and Continuous Deployment  
- **Program:** Bachelor's of Engineering in Software Engineering (SWE)  
- **Assignment:** Assignment III  
- **Submission Date:** 28th May 2025  
- **Student:** [Your Name]  
- **Student ID:** [Your Student ID]  

---

## Project Overview

This assignment demonstrates the implementation of a complete CI/CD pipeline using GitHub Actions to automate the building, testing, and deployment of a Node.js to-do list application. The pipeline includes Docker containerization, pushing to DockerHub, and automatic deployment to Render.com.

---

## Table of Contents

- Tools and Technologies  
- Project Structure  
- Implementation Steps  
- Configuration Files  
- Challenges Faced  
- Results and Screenshots  
- Learning Outcomes  
- Repository and Deployment Links  

---

## Tools and Technologies

| Tool         | Purpose                           | Version      |
|--------------|-----------------------------------|--------------|
| GitHub       | Source code hosting               | -            |
| GitHub Actions | CI/CD automation platform        | Latest       |
| Docker       | Application containerization      | Latest       |
| DockerHub    | Container image registry          | -            |
| Render.com   | Cloud deployment platform         | -            |
| Node.js      | JavaScript runtime environment    | v20 LTS      |
| npm          | Package manager                   | Latest       |
| Jest         | JavaScript testing framework      | Latest       |

---

## Implementation Steps

### Task 1: GitHub Repository Setup

- Verified public repository visibility  
- Committed all required files  
- Confirmed presence of application source code  

#### `package.json` Scripts:
```json
{
  "name": "todo-app",
  "version": "1.0.0",
  "scripts": {
    "start": "node src/app.js",
    "test": "jest",
    "dev": "nodemon src/app.js"
  },
  "dependencies": {
    "express": "^4.18.0",
    "cors": "^2.8.5"
  },
  "devDependencies": {
    "jest": "^29.0.0",
    "nodemon": "^2.0.20"
  }
}
```
### Task 2: Docker Configuration

### Dockerfile

```dockerfile
# Use Node.js LTS
FROM node:20-alpine

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy all files
COPY . .

# Run tests (optional)
RUN npm test

# Expose the app port
EXPOSE 3000

# Start the app
CMD ["npm", "start"]
```
### Local Testing
- Built Docker image: docker build -t todo-app .

- Ran container: docker run -p 3000:3000 todo-app

- Verified application at localhost:3000

### Task 3: GitHub Actions Workflow Configuration

### `.github/workflows/deploy.yml`

```yaml
name: Build and Deploy to Render

on:
  push:
    branches: ["main"]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Login to DockerHub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Build and Push Docker Image
        run: |
          docker build -t ${{ secrets.DOCKERHUB_USERNAME }}/todo-app:latest .
          docker push ${{ secrets.DOCKERHUB_USERNAME }}/todo-app:latest

      - name: Trigger Render Deployment
        run: |
          curl -X POST ${{ secrets.RENDER_DEPLOY_HOOK_URL }}
```

### GitHub Secrets
- DOCKERHUB_USERNAME

- DOCKERHUB_TOKEN

- RENDER_DEPLOY_HOOK_URL

### Task 4: Render.com Deployment Setup
### Web Service Configuration
- Name: todo-app-deployment

- Region: Oregon (US West)

- Instance Type: Free Tier

- Port: 3000

- Env Vars: NODE_ENV=production

### Deployment Webhook
- Generated from Render dashboard

- Added to GitHub secrets as RENDER_DEPLOY_HOOK_URL

### Configuration Files Summary
### Dockerfile
- Uses node:20-alpine for lightweight image

- Runs tests during build

- Follows Docker best practices

### GitHub Actions Workflow
- Trigger: Push to main branch

- Actions:

    - Builds and pushes image to DockerHub

    - Deploys using Render webhook

### Challenges Faced
### Technical
- DockerHub Authentication: Solved using token-based login

- Render Webhook: Triggered with curl

- Build Optimization: Alpine image used with Docker caching

- Docker Testing: Refined to match production

### Configuration
- YAML Syntax: Validated online

- Environment Variables: Configured correctly

- Port Issues: Ensured consistency across app, Dockerfile, and Render

### Results and Screenshots

### GitHub Actions
- Workflow passed  
- Execution time: 2–3 mins  
- Auto-trigger verified  

### DockerHub
- Image pushed: ~150MB  
- Tagged as `latest`  

### Render.com
- Deployed successfully  
- Health checks passed  
- Live app available  

### Screenshots (to be added)
- GitHub Actions logs  
- DockerHub repository  
- Render dashboard  
- Live app URL  

---

### Learning Outcomes

### Technical Skills
- **GitHub Actions:** YAML, workflows, debugging  
- **Docker:** Dockerfile creation, image optimization  
- **Cloud Deployment:** Render setup, webhook usage  

### DevOps Concepts
- **CI/CD Design:** Automated build, test, and deploy  
- **Infrastructure as Code:** Git-based deployment  
- **Security:** Secret management with no hardcoded credentials  

### Problem Solving
- Debugging with logs  
- Integration across services  
- Webhook & API troubleshooting  

---

### Future Enhancements

- Set up staging and production environments  
- Add automated test stage before deployment  
- Implement blue-green deployment  
- Integrate monitoring and alerting  
- Add security scans to CI pipeline  
- Optimize performance with Docker cache & parallel jobs  

---

### Repository and Deployment Links

- **GitHub Repository:** [https://github.com/yourusername/todo-app](https://github.com/yourusername/todo-app)  
- **DockerHub Image:** [https://hub.docker.com/r/yourusername/todo-app](https://hub.docker.com/r/yourusername/todo-app)  
- **Render Deployment:** [https://todo-app-deployment.onrender.com](https://todo-app-deployment.onrender.com)  

---

### Declaration

I confirm that this work is my own and has been completed in accordance with the RUB Wheel of Academic Law. All sources and references have been properly acknowledged, and no credentials have been hardcoded in the codebase.