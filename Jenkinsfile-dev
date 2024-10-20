pipeline {
    agent any
    tools {
        maven 'Maven3.9.9'
        jdk 'Java17'
    }
    stages {
        stage('Download-Code-GIT') {
            steps {
                echo "Download code from git"
                git branch: 'main', url: 'https://github.com/Clyde-Bunyan/maven-jenkins4.git'
            }
        }
        stage('Build') {
            steps {
                echo "Build Java Project using maven"
                sh 'mvn clean package'
            }
        }
        stage('Archive-Artifact') {
            steps {
                echo "Archiving the artifacts"
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('Trigger-Deploy-Job') {
            steps {
                echo "Triggering deploy Job"
                build wait: false, job: 'pipeline-deploy'
            }
        }
    }
}

