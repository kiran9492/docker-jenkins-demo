# Jenkins CI/CD with Docker - Flask Application

## Objective
The purpose of this project is to learn how to use **Jenkins** to build and run a **Dockerized application**, understanding the basics of **CI/CD (Continuous Integration/Continuous Deployment) with Docker**.  

By completing this project, you will gain practical experience in:  
- Automating builds using Jenkins pipelines  
- Containerizing applications with Docker  
- Deploying applications using Docker containers  
- Integrating source control (Git) with CI/CD workflows  

---

## Tools & Technologies
| Tool | Purpose |
|------|---------|
| **Jenkins** | Automate builds, run pipelines, and implement CI/CD |
| **Docker** | Containerize applications and run isolated environments |
| **Docker Compose** | Optional: Manage multi-container applications |
| **Git** | Version control for source code |
| **Python Flask / Node.js Express / Java Spring Boot** | Example application framework |
| **Operating System** | Linux preferred, or Windows with Docker Desktop |

---

## Deliverables
The project produces a **Dockerized application** with a Jenkins pipeline that automatically builds and runs the application.  

- **Application Options:**  
  - Python Flask  
  - Node.js Express  
  - Java Spring Boot  

- **CI/CD Pipeline:**  
  - Build Docker image from source code  
  - Run Docker container with the built image  
  - Deploy the application automatically  

---

## Project Structure (Example: Flask App)


---

## Setup Instructions

### Step 1: Install Required Tools
- **Docker**: [https://www.docker.com/get-started](https://www.docker.com/get-started)  
- **Jenkins**: Run locally or via Docker  
- **Git**: [https://git-scm.com/](https://git-scm.com/)

---

## Step 2: Clone Repository
git clone https://github.com/your-username/flask-jenkins-docker.git
cd flask-jenkins-docker

## Step 3: Dockerize the Application
Dockerfile (Example: Flask)
FROM python:3.10-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY app.py .
EXPOSE 5000

CMD ["python", "app.py"]

## Build and Run Docker Container
docker build -t flask-app .
docker run -d -p 5000:5000 flask-app


## Open browser:

http://localhost:5000


## You should see:

Hello from Flask App - Jenkins CI/CD!

## Step 4: Run Jenkins
Option 1: Jenkins in Docker
 docker run -d \
  --name jenkins \
  -p 8080:8080 -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkins/jenkins:lts


Access Jenkins: http://localhost:8080

Get initial admin password:

docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword


Install suggested plugins

Create admin user

## Step 5: Create Jenkins Pipeline
Jenkinsfile (Declarative Pipeline)
pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/your-username/flask-jenkins-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-jenkins-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker stop flask-jenkins || true
                docker rm flask-jenkins || true
                docker run -d -p 5000:5000 --name flask-jenkins flask-jenkins-app
                '''
            }
        }
    }
}

## Step 6: Configure Jenkins Job

1.Jenkins Dashboard → New Item → Pipeline

2.Name: Flask-CI-CD

3.Pipeline → Definition → Pipeline script from SCM

4.SCM → Git → Repository URL → https://github.com/your-username/flask-jenkins-docker.git

5.Branch → main

6.Credentials → None (if repo is public)

7.Save → Build Now

### Step 7: Verify CI/CD

1.Jenkins will build the Docker image

2.Run container automatically

3.Open browser: http://localhost:5000
 → App should be live

## Notes & Best Practices

1 .Always mount Docker socket if Jenkins runs in Docker (-v /var/run/docker.sock:/var/run/docker.sock)

2 .Name your Jenkinsfile exactly Jenkinsfile in the root repo

3 .Use public GitHub repo for simplicity; private repo requires credentials

4 .Stop old containers to avoid port conflicts:

docker stop flask-jenkins || true
docker rm flask-jenkins || true

## References

 * Jenkins Official Documentation

 * Docker Official Documentation

 * Flask Official Documentation

 * Docker & Jenkins CI/CD Tutorial

## Deliverables Checklist

 *  Python Flask / Node.js / 

 *  Dockerfile

 * Jenkinsfile
 
 * Jenkins Pipeline running successfully

 * Docker container deployed and accessible


### This README covers:  
✅ Objective  
✅ Tools  
✅ Project structure  
✅ Step-by-step setup  
✅ Jenkinsfile example  
✅ CI/CD verification  
✅ Best practices & references  

---




<img width="1366" height="768" alt="Screenshot (103)" src="https://github.com/user-attachments/assets/d825cf4f-9555-4c26-bfd1-f701148ce284" />


