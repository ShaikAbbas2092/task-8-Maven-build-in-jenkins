
# hello-java-maven Jenkins Pipeline Project

This project demonstrates how to build a simple Java Maven application using Jenkins Pipeline.

## Project Contents
- `src/main/java/HelloWorld.java` — Java source printing "Hello, Jenkins + Maven!"
- `pom.xml` — Maven project configuration file
- `Jenkinsfile` — Declarative Jenkins Pipeline to build and test the app

## Prerequisites
- Jenkins installed with Maven and JDK configured via Manage Jenkins → Global Tool Configuration
- Git repository containing this project
- Correct tool names in `Jenkinsfile` matching Jenkins configuration

## Pipeline Overview
The pipeline performs:
1. Checkout from Git
2. Maven clean and package
3. Maven test
4. Post-build status notifications

## Usage Instructions

### Clone repository
```
git clone https://github.com/your-username/hello-java-maven.git
cd hello-java-maven
```

### Configure Jenkins
- In Jenkins, ensure Maven and JDK tool installations exist and note their names.
- Create a new Pipeline job in Jenkins.
- Under Pipeline section, select "Pipeline script".
- write declarative pipeline as shown below.
-
'''
  pipeline {
    agent any

    tools {
        maven 'updated version'  // Name of Maven installation in Jenkins Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from Git; adjust URL and branch as needed
                git branch: 'main', url: 'https://github.com/ShaikAbbas2092/task-8-Maven-build-in-jenkins.git'
            }
        }

        stage('Build') {
            steps {
                // Run Maven clean package without tests
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                // Optionally run tests
                sh 'mvn test'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}

'''
- Save the job.

### Run the Pipeline
- Click "Build Now" in Jenkins to start the build.
- View progress and logs through Jenkins Web UI.
- Successful build logs include `BUILD SUCCESS`.

## Maven Useful Commands
- Clean and package:
```
mvn clean package
```
- Run tests:
```
mvn test
```

## Git Commands for Updating Repo
```
git add .
git commit -m "Add Jenkinsfile and source code"
git push origin main
```

---

**Note:** Ensure Maven and JDK names in the pipeline script align exactly with Jenkins Global Tool Configuration to avoid build errors.

Happy CI/CD with Jenkins and Maven!
```
