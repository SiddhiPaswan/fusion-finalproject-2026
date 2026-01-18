## Introduction

This document explains a Jenkins CI/CD pipeline used to automate the process of building, containerizing, and deploying an application to a Kubernetes (EKS) cluster.

The pipeline integrates multiple DevOps tools such as **Git**, **Maven**, **Docker**, **AWS**, and **Kubernetes** to achieve continuous integration and continuous deployment. From pulling the latest source code to deploying the updated application on Kubernetes, every step is fully automated.

This approach ensures:
- Faster and consistent deployments  
- Reduced manual errors  
- Easy version control using Docker image tags  
- Reliable application rollout on Kubernetes  

The following sections describe each pipeline stage in detail and explain how Jenkins orchestrates the complete CI/CD workflow.

### Pipeline Snippet
  **Jenkins CI/CD Pipeline – Stage-wise Explanation**
    This Jenkins pipeline automates the complete CI/CD process starting from source code checkout to deployment on a Kubernetes cluster.
````

pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "siddhipaswan/myimage"
    }

    stages {

        stage('Git Checkout') {
            steps {
                git 'https://github.com/SiddhiPaswan/fusion-final-project-2026.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh """
                docker build -t ${DOCKER_IMAGE}:${BUILD_NUMBER} .
                """
            }
        }

        stage('Docker Push') {
            steps {
                sh """
                docker push ${DOCKER_IMAGE}:${BUILD_NUMBER}
                """
            }
        }

        stage('Update Deployment Image') {
            steps {
                sh """
                sed -i 's|image: siddhipaswan/.*|image: ${DOCKER_IMAGE}:${BUILD_NUMBER}|' deployments.yml
                """
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh """
                kubectl apply -f deployments.yml
                kubectl rollout restart deployment mywebdeployment
                """
            }
        }
    }
}

````

### Pipeline Stages
**Stage 1: Git Checkout**
```
stage('Git Checkout') {
    steps {
        git 'https://github.com/SiddhiPaswan/fusion-final-project-2026.git'
    }
}

```
Clones the source code from the GitHub repository.
Ensures Jenkins always builds the latest version of the code.
This is the starting point of the CI pipeline.

**Stage 2: Maven Build**
```
stage('Maven Build') {
    steps {
        sh 'mvn clean package'
    }
}
```
This stage builds the application using Maven.
mvn clean removes previous build artifacts
mvn package compiles the source code and generates a deployable JAR/WAR file
If the build fails, the pipeline stops immediately, ensuring code quality

**Stage 3: Docker Build**
```
stage('Docker Build') {
    steps {
        sh """
        docker build -t ${DOCKER_IMAGE}:${BUILD_NUMBER} .
        """
    }
}
```
This stage creates a Docker image from the application.
Uses the Dockerfile present in the repository
Tags the image with the Jenkins BUILD_NUMBER
Provides versioning for each application build

**Stage 4: Docker Push**
```
stage('Docker Push') {
    steps {
        sh """
        docker push ${DOCKER_IMAGE}:${BUILD_NUMBER}
        """
    }
}
```

This stage uploads the Docker image to Docker Hub.
Makes the image accessible to Kubernetes
Acts as a bridge between CI and CD
Ensures the deployment uses a centralized image repository

**Stage 5: Update Deployment Image**
```
stage('Update Deployment Image') {
    steps {
        sh """
        sed -i 's|image: siddhipaswan/.*|image: ${DOCKER_IMAGE}:${BUILD_NUMBER}|' deployments.yml
        """
    }
}

```
This stage updates the Kubernetes deployment file.

Replaces the old Docker image with the newly built image

Ensures Kubernetes always deploys the latest application version

Avoids manual modification of YAML files

**Stage 6: Deploy to Kubernetes**
```
stage('Deploy to Kubernetes') {
    steps {
        sh """
        kubectl apply -f deployments.yml
        kubectl rollout restart deployment mywebdeployment
        """
    }
}

```
This stage deploys the application to the Kubernetes cluster.

kubectl apply creates or updates the deployment

kubectl rollout restart triggers Kubernetes to pull the new Docker image

Completes the Continuous Deployment (CD) process