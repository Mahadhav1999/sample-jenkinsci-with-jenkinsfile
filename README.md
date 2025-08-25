# 🚀 Sample Jenkins CI with Jenkinsfile

This repository provides a **comprehensive walkthrough** for setting up Jenkins on **Google Cloud Platform (GCP)** and integrating it with a **GitHub repository** containing a `Jenkinsfile`.

Whether you’re new to **Jenkins** or **GCP**, this guide will help you set up a working Continuous Integration (CI) pipeline quickly.

---

## ✅ Prerequisites

Before starting, ensure you have:

* A **Google Cloud account** with Compute Engine enabled.
* A **GitHub account**.
* Basic knowledge of Linux commands.
* A sample GitHub repository with some **Java code** (or any language) and a **Jenkinsfile**.

---

## 📝 Step-by-Step Setup

### **Step 1: Create a Sample GitHub Repository**

1. Go to [GitHub](https://github.com/new) → create a new repository.
   Example: `sample-jenkinsci-with-jenkinsfile`.
2. Add some sample Java (or Python/Node) code.
   Example: `HelloWorld.java`.
3. Create a file named **`Jenkinsfile`** at the root of the repo with a minimal pipeline:

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}
```

✅ Ensure the filename is exactly `Jenkinsfile` (case-sensitive).

---

### **Step 2: Create a VM on GCP & Install Jenkins**

1. Go to **GCP Console** → Compute Engine → VM Instances → **Create Instance**.

   * Name: `jenkins-ci`
   * Machine type: `e2-medium` (2 vCPUs, 4GB RAM)
   * Boot disk: Ubuntu 22.04 LTS
   * Allow **HTTP & HTTPS traffic**
2. SSH into VM and install Jenkins.
   You can follow this guide 👉 [Jenkins Setup and Installation](https://github.com/Mahadhav1999/jenkins-setup-and-installation).

---

### **Step 3: Access Jenkins UI**

1. Get VM **External IP** from GCP.
2. Open in browser:

   ```
   http://<external-ip>:8080
   ```
3. Unlock Jenkins:

   ```bash
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   ```
4. Install **suggested plugins** and create an **Admin user**.

---

### **Step 4: Create a New Pipeline Job in Jenkins**

1. Go to Jenkins Dashboard → Click **New Item**.
2. Enter job name: `first-pipeline-job-with-jenkinsfile`.
3. Select **Pipeline** → Click OK.

---

### **Step 5: Configure GitHub Repository in Jenkins**

1. In job configuration → Scroll to **Pipeline** section.
2. Set **Definition** → *Pipeline script from SCM*.
3. SCM → Select **Git**.
4. Enter your **GitHub Repository URL**.
   Example:

   ```
   https://github.com/<your-username>/sample-jenkinsci-with-jenkinsfile.git
   ```
5. If repo is private → click **Add Credentials** → provide GitHub username & token.

---

### **Step 6: Configure Branch & Script Path**

1. Scroll to **Branches to build** section.

   * Branch Specifier: `main` (or `master`, depending on your repo).
2. Scroll to **Script Path** → set as `Jenkinsfile`.

⚠️ **Important**: The filename in GitHub and Script Path must match exactly (case-sensitive).

---

### **Step 7: Save & Build**

1. Click **Save**.
2. Go to job dashboard → Click **Build Now**.
3. Open **Console Output** → Jenkins will show logs of each stage (Build, Test, Deploy).

---

### **Step 8: Verify Build Status**

* ✅ **SUCCESS** → All stages executed properly.
* ❌ **FAILURE** → Build or Test step failed.
* ⚠️ **UNSTABLE** → Build successful but some tests failed.

---


## 🎯 Final Result

You now have a **Jenkins CI Pipeline** on **GCP VM** that:

* Pulls code from GitHub.
* Runs Build, Test, Deploy stages via `Jenkinsfile`.
* Can auto-trigger builds using webhooks or pollSCM configuration.

---

