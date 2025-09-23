#  Jenkins CI/CD Pipeline for Spring Boot + Docker + SonarQube + Argo CD

This repository demonstrates a robust, production-grade CI/CD pipeline for a Spring Boot application, leveraging Jenkins, Docker, SonarQube, and GitOps with Argo CD. The pipeline automates the process from code commit to deployment on Kubernetes, ensuring code quality, security, and rapid delivery.

---

## Pipeline Architecture

![image alt](https://github.com/Zayn-Mohamad/springboot-devops-pipeline/blob/e873dfc6b0a22af15ba91b8fcec98fd4c1ccfaca/Untitled%20Diagram.drawio(2).png)

---

## Technologies Used

- **Jenkins**: Orchestrates the CI/CD pipeline using Pipeline as Code (Jenkinsfile).
- **Maven**: Builds and tests the Java Spring Boot application.
- **SonarQube**: Performs static code analysis to ensure code quality and security.
- **Docker**: Packages the application into a container image.
- **Docker Hub**: Stores and distributes the Docker images.
- **GitHub**: Hosts the source code and Kubernetes manifests (GitOps).
- **Argo CD**: Automates deployment to Kubernetes using GitOps principles.
- **Kubernetes**: Runs the application in a scalable, production-ready environment.

---

##  Pipeline Stages Explained

1. **Source Code Commit**
    - Developers push code changes to the GitHub repository.

2. **Jenkins Trigger**
    - Jenkins is configured to listen for changes (webhook or polling).
    - On new commits, Jenkins triggers the pipeline.

3. **Build & Test with Maven**
    - Jenkins uses Maven to compile the code and run unit/integration tests.
    - Ensures the application is functional and stable before proceeding.

4. **Static Code Analysis with SonarQube**
    - Jenkins runs SonarQube analysis on the codebase.
    - Detects bugs, code smells, and security vulnerabilities.
    - Fails the build if quality gates are not met.

5. **Docker Image Build**
    - Jenkins builds a Docker image of the Spring Boot application.
    - The image is tagged with the commit SHA or build number for traceability.

6. **Push Image to Docker Hub**
    - The built Docker image is pushed to Docker Hub (or another registry).
    - Credentials are securely managed in Jenkins.

7. **Update Kubernetes Manifest**
    - Jenkins updates the Kubernetes deployment manifest (e.g., image tag).
    - The manifest is committed and pushed to a separate GitOps repository.

8. **Argo CD Sync**
    - Argo CD monitors the GitOps repository for changes.
    - On detecting a new commit, Argo CD syncs the Kubernetes cluster state to match the manifest.
    - The new version of the application is deployed automatically.

---

##  Prerequisites

- Jenkins server with required plugins (Pipeline, Docker, Git, SonarQube, etc.)
- SonarQube server (local or cloud)
- Docker Hub account (or other registry)
- Kubernetes cluster (e.g., Minikube, EKS, GKE, AKS)
- Argo CD installed and configured
- GitHub repositories for source code and GitOps manifests

---

##  Setup & Usage

1. **Clone the Repository**
    ```bash
    git clone https://github.com/your-org/your-repo.git
    cd your-repo
    ```

2. **Configure Jenkins**
    - Set up credentials for GitHub, Docker Hub, and SonarQube.
    - Create a new pipeline job using the provided `Jenkinsfile`.

3. **Configure SonarQube**
    - Create a new project in SonarQube.
    - Update the `Jenkinsfile` with the correct SonarQube project key and server URL.

4. **Configure Docker Hub**
    - Create a repository for your Docker images.
    - Add Docker Hub credentials to Jenkins.

5. **Configure Kubernetes & Argo CD**
    - Deploy Argo CD to your Kubernetes cluster.
    - Connect Argo CD to your GitOps repository containing the Kubernetes manifests.

6. **Run the Pipeline**
    - Push a code change to GitHub.
    - Jenkins will automatically trigger the pipeline, build, test, analyze, package, and deploy your application.

---

##  Security & Best Practices

- Use Jenkins credentials binding for all secrets.
- Enforce SonarQube quality gates to prevent bad code from being deployed.
- Tag Docker images with unique identifiers (e.g., commit SHA).
- Use separate repositories for application code and deployment manifests (GitOps).
- Enable RBAC and network policies in Kubernetes for secure deployments.

---

##  References

- [Jenkins Documentation](https://www.jenkins.io/doc/)
- [SonarQube Documentation](https://docs.sonarqube.org/)
- [Docker Documentation](https://docs.docker.com/)
- [Argo CD Documentation](https://argo-cd.readthedocs.io/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)

---

## 🤝 Contributing

Contributions are welcome! Please open issues or submit pull requests for improvements, bug fixes, or new features.

---

## 📝 License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
