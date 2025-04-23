
## Hello world python app
This is a python app which is written in python for understanding of Jenkins and gitlab continuous integration and continuous deployment.

# Hello World CI

## Summary

The **Hello World** project is a simple demonstration of continuous integration (CI) using **Jenkins** and **GitLab**. The goal of this project is to automate the process of creating a Docker image and pushing it to Docker Hub whenever a developer commits new changes on **GitLab**.

## Workflow

1. **Push New Code to GitLab**  
   The developer commits code to the GitLab repository.

2. **Create CI Pipeline in Jenkins**  
   The Jenkins pipeline is set up to trigger on code changes and automatically build the Docker image.

3. **Create Docker Image**  
   Jenkins uses a **Dockerfile** to build a Docker image of the application.

4. **Push Docker Image to Docker Hub**  
   Once the Docker image is built, it is pushed to Docker Hub for storage and deployment.

## Detailed Explanation

### 1. GitLab

- The code is written in **Python** and utilizes **Flask** to build a simple web application.
- Flask's main application file is located at:  
  `~/app.py`

### 2. Jenkins Pipeline

The Jenkins pipeline automates the process of building and pushing the Docker image. Below are the steps to set up the Jenkins pipeline:

#### Steps to Set Up Jenkins Pipeline:

- **Step 1**: Add your GitLab and Docker Hub credentials in Jenkins.  
  Go to **Manage Jenkins** > **Credentials** > **System** > **Global credentials** > **Add Credentials**.  
  Add your credentials with appropriate ID names for later use in the Jenkinsfile.

- **Step 2**: Create a new Jenkins Pipeline job.  
  - Go to **New Item** > Select **Multibranch Pipeline**.  
  - Name the job accordingly (e.g., `HelloWorld-CI`).
  - Under **Branch Sources**, select **Git** and provide your GitLab repository URL.  
  - Add your GitLab credentials for access.

- **Step 3**: Configure the **Jenkinsfile** in your GitLab repository.  
  The Jenkinsfile will define the pipeline for your CI process. Ensure that the file is placed in the root of your GitLab repository.

- **Step 4**: Enable **Multibranch Pipeline Scan Triggers**.  
  This will automatically scan your repository for branches and trigger builds. Set it to scan every **1 minute**.

### 3. Jenkinsfile

The **Jenkinsfile** defines the steps to automate the build process, from cloning the Git repository to pushing the Docker image to Docker Hub.

Here's the structure of the Jenkinsfile:

```groovy
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "yourdockerhubusername/helloworld-python:latest"
        GIT_REPO = 'http://your.gitlab.server/yourrepo.git'
        GIT_BRANCH = 'main'
    }

    stages {
        stage('Checkout and Build') {
            steps {
                script {
                    // Checkout code and build Docker image
                    withCredentials([usernamePassword(credentialsId: 'gitlab_id', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                        sh """
                            git clone http://\$GIT_USERNAME:\$GIT_PASSWORD@$GIT_REPO
                            cd helloworld-ci
                            git checkout \$GIT_BRANCH
                            docker build -t ${DOCKER_IMAGE} .
                        """
                    }
                }
            }
        }

        stage('Login and Push Docker Image') {
            steps {
                script {
                    // Login to Docker Hub and push the image
                    withCredentials([usernamePassword(credentialsId: 'dockerhub_id', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh """
                            docker login -u \$DOCKER_USERNAME -p \$DOCKER_PASSWORD
                            docker push ${DOCKER_IMAGE}
                        """
                    }
                }
            }
        }
    }

    post {
        always {
            // Clean up the Docker image after pushing
            sh "docker rmi ${DOCKER_IMAGE}"
        }

        success {
            echo "Docker image successfully pushed."
        }

        failure {
            echo "Error during the build process."
        }
    }
}