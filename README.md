# End-to-End Jenkins CI/CD Pipeline for a Spring Boot Application

An end-to-end CI/CD pipeline for a Java Spring Boot application using **Jenkins, Maven, SonarQube, Docker, Trivy, Docker Hub, AWS EC2, Terraform, and Jenkins Shared Libraries**.

The pipeline automates the application delivery process from source-code checkout through testing, code analysis, Docker image creation, security scanning, and Docker Hub publishing.

---

## Architecture

```text
                    GitHub
                       |
                       v
                  +---------+
                  | Jenkins |
                  | AWS EC2 |
                  +----+----+
                       |
        +--------------+--------------+
        |              |              |
        v              v              v
    Unit Tests    SonarQube       Maven Build
        |         Analysis            |
        |              |               |
        |         Quality Gate         |
        |              |               |
        +--------------+---------------+
                       |
                       v
                 Docker Build
                       |
                       v
                 Trivy Scan
                       |
                       v
                  Docker Hub
                       |
                       v
                 Image Cleanup
```

---

## Technology Stack

| Category               | Technology             |
| ---------------------- | ---------------------- |
| CI/CD                  | Jenkins                |
| Source Control         | Git / GitHub           |
| Application            | Spring Boot            |
| Language               | Java 21                |
| Build Tool             | Maven 3.9.12           |
| Code Quality           | SonarQube              |
| Containerization       | Docker                 |
| Security Scanning      | Trivy                  |
| Container Registry     | Docker Hub             |
| Cloud                  | AWS                    |
| Infrastructure as Code | Terraform              |
| OS                     | Linux                  |
| Pipeline Reuse         | Jenkins Shared Library |

---

## Application

**Application:** `springboot-cicd-app`

The application is a Spring Boot application packaged as a JAR using Maven.

Key technologies include:

* Java 21
* Spring Boot 3.2.5
* Spring Cloud
* Spring Boot Web
* Spring Boot Actuator
* Spring Cloud Kubernetes Configuration
* Maven

---

## CI/CD Pipeline

The Jenkins pipeline consists of the following stages:

```text
1. Git Checkout
2. Unit Tests
3. Integration / Verification Tests
4. SonarQube Static Code Analysis
5. SonarQube Quality Gate
6. Maven Build
7. Docker Image Build
8. Trivy Vulnerability Scan
9. Docker Hub Push
10. Docker Image Cleanup
```

The pipeline uses Jenkins parameters for the Docker image configuration:

```text
DockerImageName = springboot-cicd-app
DockerImageTag  = 1.0.0
DockerHubUser   = shyamsunder01
```

Resulting image:

```text
shyamsunder01/springboot-cicd-app:1.0.0
```

---

## Jenkins Shared Library

The pipeline uses a reusable Jenkins Shared Library:

```text
my-shared-library
```

Reusable functions include:

```text
gitCheckout()
mvnTest()
mvnIntegrationTest()
statiCodeAnalysis()
QualityGateStatus()
mvnBuild()
dockerBuild()
dockerImageScan()
dockerImageCleanup()
```

This keeps the Jenkinsfile focused on pipeline orchestration while common operations are maintained separately.

---

## Quality & Security

### SonarQube

The pipeline performs static code analysis and validates the Quality Gate.

Current successful analysis:

```text
Quality Gate   : PASSED
Bugs           : 0
Vulnerabilities: 0
Code Smells    : 0
Duplications   : 0.0%
```

### Trivy

Before publishing the image, the generated Docker image is scanned using Trivy for container vulnerabilities.

---

## AWS Infrastructure

The Jenkins server runs on an AWS EC2 instance provisioned using Terraform.

```text
Region        : ap-south-1
Instance Type : m7i-flex.large
Instance Name : Pipeline-Server
```

AWS Systems Manager is used for instance connectivity through an IAM role.

---

## Project Structure

```text
.
├── src/
│   ├── main/
│   │   ├── fabric8/
│   │   ├── java/
│   │   └── resources/
│   └── test/
│
├── Dockerfile
├── Jenkinsfile
├── pom.xml
├── deployment.yaml
├── mvnw
├── mvnw.cmd
└── README.md
```

---

## Key DevOps Practices Demonstrated

* Jenkins Declarative Pipeline
* Jenkins Shared Libraries
* CI/CD automation
* GitHub SSH integration
* Maven build and test automation
* SonarQube static analysis
* Quality Gate validation
* Docker image creation
* Trivy vulnerability scanning
* Docker Hub image publishing
* Jenkins Credentials
* AWS EC2
* Terraform
* Linux administration
* CI/CD troubleshooting

---

## Current Improvements Planned

* Add JaCoCo test coverage reporting.
* Update Docker runtime image to Java 21.
* Improve automated Docker image versioning.
* Consolidate Docker Hub push into the Jenkins Shared Library.
* Add automated deployment after successful image publication.

---

## Docker Image

The application image is published to Docker Hub:

**Image:**

```text
shyamsunder01/springboot-cicd-app:1.0.0
```

---

## Project Status

**CI/CD Pipeline:** Completed

All current pipeline stages execute successfully from source checkout through Docker image publication and cleanup.

---

## Author

**Shyam Sunder**

SRE / DevOps Engineer

Focused on:

`AWS | Kubernetes | Docker | Jenkins | CI/CD | Linux | Terraform | Ansible`
