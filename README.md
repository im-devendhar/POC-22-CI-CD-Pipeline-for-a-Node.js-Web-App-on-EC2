
***

# **CI/CD Pipeline for Deploying a Node.js Web Application on EC2 Using GitHub Actions and Docker**

***

## ** 1. Overview**

This POC covers:

*   Creating an EC2 Ubuntu instance
*   Installing Docker
*   Building a Node.js application
*   Containerizing using Docker
*   Setting up GitHub Actions
*   Using Docker Hub as registry
*   Deploying on EC2 via a self-hosted GitHub Runner
*   Triggering automated deployments with every code push

***

## ** 2. Steps Performed**

### **Step 1: Created an EC2 Ubuntu Instance**

*   Launched an Ubuntu EC2 instance on AWS.
*   Allowed inbound rules for:
    *   **SSH (22)**
    *   **HTTP (80)**
*   Connected to the instance via SSH.

***

### **Step 2: Installed Docker on the EC2 Instance**

Installed Docker so the instance can run containers.

Verified using:

```bash
docker --version
```

***

### **Step 3: Created a Basic Node.js Application**

Developed a simple Node.js backend server (e.g., `server.js`) listening on port **3000**.

Tested locally using:

```bash
node server.js
```

***

### **Step 4: Containerized the Application Using Docker**

Created a Dockerfile that:

*   Uses Node.js base image
*   Installs dependencies
*   Copies application code
*   Exposes port 3000
*   Starts the application

This ensures the app runs consistently in a container.

***

### **Step 5: Created a GitHub Actions CI/CD Pipeline**

Added a GitHub Actions workflow that performs:

1.  Checkout code
2.  Build Docker image
3.  Push image to Docker Hub
4.  Deploy on EC2 using self-hosted runner
5.  Stop old container & run new one

This automates the deployment process.

***

### **Step 6: Configured GitHub Secrets**

Added the following secrets in GitHub repository:

*   `DOCKER_USERNAME`
*   `DOCKER_PASSWORD` (token recommended)
*   `DOCKER_REPO` (e.g., `node-app`)

These secrets are used inside the CI/CD pipeline.

***

### **Step 7: Installed GitHub Self-Hosted Runner on EC2**

Configured GitHub Actions Runner on the EC2 instance so the workflow can deploy locally.

Steps:

*   Download runner package
*   Configure repository token
*   Install as system service
*   Start the runner

***

### **Step 8: Triggered and Verified the Pipeline**

*   Initial run had indentation issues → fixed them
*   Full pipeline ran successfully:
    *   Image built
    *   Image pushed to Docker Hub
    *   EC2 pulled the new image
    *   Old container removed
    *   New container started

Deployment completed.

***

### **Step 9: Made Code Changes to Test Redeployment**

*   Updated Node.js app
*   Pushed to GitHub → CI/CD pipeline re-triggered
*   New image created
*   EC2 automatically replaced old container

This confirmed that automated deployments work end-to-end.

***

### **Step 10: Accessed the Application in Browser**

Since Docker maps:

    HOST PORT 80 → CONTAINER PORT 3000

Opened the app using EC2 Public IP:

    http://<EC2-Public-IP>

Successfully verified the web application after deployment.

***

## ** 3. Final Outcome**

✔ Node.js application successfully dockerized  
✔ Fully automated CI/CD pipeline using GitHub Actions  
✔ Docker Hub used as image registry  
✔ Self-hosted runner deployed on EC2  
✔ Auto-deployment on every push to `main`  
✔ Application accessible via EC2 public IP

***


