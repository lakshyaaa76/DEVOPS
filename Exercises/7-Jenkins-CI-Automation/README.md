# Exercise 7 – Jenkins CI Automation

## Objective

Understand the concept of Continuous Integration (CI), then install and run Jenkins as a Docker container, unlock it using the initial admin password, and access the Jenkins dashboard through a web browser.

## Environment

* OS: Windows 11
* Shell: PowerShell (VS Code terminal)
* Container Runtime: Docker
* Image: `jenkins/jenkins:lts`
* Jenkins Version: 2.580.1
* Access URL: `http://localhost:8080`

## 1. What is Continuous Integration (CI)?

Continuous Integration is a development practice where developers frequently integrate their code changes into a shared repository. Each integration triggers an automated build and test run, so errors are detected early and fixed quickly.

Key features of CI:

* Frequent code integration into a shared repository.
* Automated builds on every commit.
* Automated testing to ensure existing functionality remains intact.
* Immediate feedback to developers.

Benefits of CI:

* Early bug detection, which reduces the cost of fixing bugs.
* Better collaboration on a shared codebase.
* Faster development cycles.
* Higher code quality and fewer regressions.

## 2. What is Jenkins?

Jenkins is an open-source automation server used to build, test, and deploy software. It automates repetitive tasks and enables Continuous Integration (CI) and Continuous Delivery (CD).

Key Jenkins concepts:

* **Job/Project**: A task or process that Jenkins runs.
* **Build**: The process of compiling and packaging code.
* **Pipeline**: A series of steps to build, test, and deploy an application.
* **Plugins**: Extend Jenkins' functionality (for example, Git and Docker plugins).
* **Nodes**: Machines where Jenkins runs jobs (controller/agent setup).

## 3. Start Jenkins Using Docker

Run Jenkins as a container in detached mode:

```powershell
docker run -d --name jenkins -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts
```

* Port `8080` is used to access the Jenkins web interface.
* Port `50000` is used by Jenkins agents to connect to the controller.

Docker pulled the `jenkins/jenkins:lts` image and started the container.

## 4. Verify the Container

Check that the container is running:

```powershell
docker ps
```

The `jenkins` container showed an `Up` status with ports `8080` and `50000` mapped to the host.

## 5. Get the Initial Admin Password

Read the initial admin password from inside the container:

```powershell
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

The command printed the initial admin password required to unlock Jenkins.

## 6. Open Jenkins in the Browser

Open the Jenkins URL:

```powershell
Start-Process "http://localhost:8080"
```

The browser opened `http://localhost:8080`.

![Jenkins Container Setup](screenshots/01-jenkins-container-setup.png)

## 7. Unlock Jenkins

The **Unlock Jenkins** screen was displayed. It shows the path of the password file, `/var/jenkins_home/secrets/initialAdminPassword`, and a password box with a **Continue** button.

The initial admin password from Step 5 was entered to unlock Jenkins.

![Jenkins Unlock Screen](screenshots/02-jenkins-unlock-screen.png)

## 8. Complete the Setup

The setup wizard was completed. The admin user creation step was skipped, so login is done with the username `admin` and the initial admin password.

The **Jenkins is ready!** message was displayed with a **Start using Jenkins** button.

![Jenkins Setup Complete](screenshots/03-jenkins-setup-complete.png)

## 9. Jenkins Dashboard

The Jenkins dashboard opened successfully.

* Sidebar: New Item, Build History, Build Queue (empty), Build Executor Status (0/2).
* Main area: Welcome message with options to create jobs or set up distributed builds.
* Jenkins version: 2.580.1.

![Jenkins Dashboard](screenshots/04-jenkins-dashboard.png)

## 10. Jenkins CI Working

The basic CI flow with Jenkins is:

```text
Developer
   ↓
Git Repository
   ↓
Jenkins Server
   ↓
Automated Build
   ↓
Automated Tests
   ↓
Feedback (Success / Failure)
```

* The developer pushes code to the version control system (Git).
* Jenkins detects the change and triggers a build.
* The code is compiled and dependencies are resolved.
* Automated tests are run to verify functionality.
* The build and test results are sent back to the developer.

## 11. Commands Used

```powershell
cd .\Exercises\7-Jenkins-CI-Automation

docker run -d --name jenkins -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts

docker ps

docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword

Start-Process "http://localhost:8080"
```

## 12. Result

Jenkins was successfully installed and run as a Docker container on Windows 11.

The container started with ports `8080` and `50000` mapped, Jenkins was unlocked using the initial admin password, the setup completed with the **Jenkins is ready!** message, and the Jenkins dashboard was accessed through the browser at `http://localhost:8080`.