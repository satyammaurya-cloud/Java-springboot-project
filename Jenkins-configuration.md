# CI/CD Pipeline: GitHub → Jenkins → Docker → EC2

This document explains the complete CI/CD flow for deploying a Spring Boot application using GitHub, Jenkins, Docker, and EC2.

------------------------------------------------------------
1. EC2 Setup (Base Infrastructure)
------------------------------------------------------------

- Launch EC2 instance
- Install Docker
- Install Docker Compose
- Install Git
- Install Jenkins
- Add jenkins user to docker group
- Restart Docker and Jenkins

Commands:

```bash
sudo usermod -aG docker jenkins
sudo systemctl restart docker
sudo systemctl restart jenkins
```

This prepares the build server.

------------------------------------------------------------
2. GitHub Repository Setup
------------------------------------------------------------

- Push application code to GitHub
- Repository should be public (or add credentials in Jenkins)
- Add Jenkinsfile in root directory
- Use proper branch (main/master)

This prepares source control.

------------------------------------------------------------
3. Jenkins Pipeline Job Configuration
------------------------------------------------------------

- Create New Item → Pipeline
- Definition → Pipeline script from SCM
- SCM → Git
- Repository URL → Correct GitHub URL (https://github.com/satyammaurya-cloud/Java-springboot-project.git)
- Branch → */main
- Script Path → Jenkinsfile
- Lightweight checkout → Enabled

This connects Jenkins to GitHub.

------------------------------------------------------------
4. Pipeline Execution Flow
------------------------------------------------------------

When pipeline runs:

- Jenkins pulls code
- Jenkins reads Jenkinsfile
- Executes pipeline stages
- Builds Docker image
- Runs Docker containers
- Application deployed on EC2

This completes CI/CD flow.

------------------------------------------------------------
5. Permission Configuration (Critical Step)
------------------------------------------------------------

If Docker permission issue occurs:

```bash
sudo usermod -aG docker jenkins
sudo systemctl restart docker
sudo systemctl restart jenkins
```
- Jenkins added to docker group
- Docker daemon accessible
- No permission denied error

This enables Docker build from Jenkins.

------------------------------------------------------------
6. Optional Automation (Advanced)
------------------------------------------------------------

- Configure GitHub webhook
- Jenkins auto-trigger on git push
- Poll SCM configured (optional)

This enables continuous integration.

------------------------------------------------------------
Complete Flow
------------------------------------------------------------

Developer → Git Push → GitHub
GitHub → Triggers Jenkins
Jenkins → Builds Docker Image
Docker → Runs Container
Application → Deployed on EC2
