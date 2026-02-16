# GitHub Hook Trigger for GITScm Polling

## 🟢 1️⃣ Prepare Jenkins Server

✔ Jenkins installed  
✔ Git installed  
✔ Port 8080 open in Security Group  
✔ Jenkins accessible via:  

http://<EC2-IP>:8080  

**Remark:**  
Jenkins must be publicly reachable.

---

## 🟢 2️⃣ Install Required Plugins

✔ Install GitHub Integration Plugin  


**Remark:**  
GitHub Plugin is required for webhook trigger.

---

## 🟢 3️⃣ Configure Jenkins Pipeline

✔ Create New Item → Pipeline  
✔ Definition → Pipeline script from SCM  
✔ SCM → Git  
✔ Add GitHub repository URL  
✔ Branch → */main  
✔ Script Path → Jenkinsfile  
✔ Enable Lightweight checkout  

**Remark:**  
Jenkinsfile must exist in repository root.

---

## 🟢 4️⃣ Enable Webhook Trigger

✔ Go to Build Triggers  
✔ Enable: GitHub hook trigger for GITScm polling  

**Remark:**  
Without this option, webhook will not trigger build.

---

## 🟢 5️⃣ Configure GitHub Webhook

✔ GitHub → Settings → Webhooks → Add Webhook  
✔ Payload URL:

```
http://<EC2-IP>:8080/github-webhook/
```

✔ Content type → application/json  
✔ Event → Just the push event  

**Remark:**  
URL must end with `/github-webhook/`  
Port 8080 must be open.

---

## 🟢 6️⃣ Test Automation

✔ Push code to GitHub  
✔ Jenkins should auto-trigger build  

**Remark:**  
If not triggered, check:  
GitHub → Webhooks → Recent Deliveries.
