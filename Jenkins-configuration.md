✅ High-Level Steps: GitHub → Jenkins → Docker → EC2
🟢 1️⃣ EC2 Setup (Base Infrastructure)

✔ Launch EC2
✔ Install Docker
✔ Install Docker Compose
✔ Install Git
✔ Install Jenkins
✔ Add jenkins user to docker group
✔ Restart Docker & Jenkins

This prepares build server.

🟢 2️⃣ GitHub Repository Setup

✔ Application code pushed to GitHub
✔ Repository public (or credentials added in Jenkins)
✔ Jenkinsfile added in root directory
✔ Proper branch used (main/master)

This prepares source control.

🟢 3️⃣ Jenkins Pipeline Job Configuration

✔ Create New Item → Pipeline
✔ Definition → Pipeline script from SCM
✔ SCM → Git
✔ Repository URL → Correct GitHub URL
✔ Branch → */main
✔ Script Path → Jenkinsfile
✔ Lightweight checkout → Enabled

This connects Jenkins to GitHub.

🟢 4️⃣ Pipeline Execution Flow

✔ Jenkins pulls code
✔ Jenkins reads Jenkinsfile
✔ Executes pipeline stages
✔ Builds Docker image
✔ Runs Docker containers
✔ Application deployed on EC2

This completes CI/CD flow.

🟢 5️⃣ Permission Configuration (Critical)

✔ jenkins added to docker group
✔ Docker daemon accessible
✔ No permission denied error
'''
sudo usermod -aG docker jenkins
sudo systemctl restart docker
sudo systemctl restart jenkins
'''

This enables Docker build from Jenkins.

🟢 6️⃣ Optional Automation (Advanced)

✔ GitHub webhook configured
✔ Jenkins auto-trigger on git push
✔ Poll SCM configured (optional)

This enables continuous integration.
