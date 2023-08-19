
pipeline {
    agent any
    tools {
        maven '3.6.3'
    }
    stages {
        stage("Source") {
            steps {
                git branch: 'main', url: 'https://github.com/zoudoum/tpjenskin.git'
            }
        }
        stage("Build") {
            steps {
                sh 'mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install'
            }
        }
        stage("SonarQube Analysis") {
            steps {
                sh 'mvn sonar:sonar'
            }
        }
        stage('Approve Deployment') {
            input {
                message "Do you want to proceed for deployment?"
            }
            steps {
                sh 'echo "Deploying into Server"'
            }
        }
    }
    post {
        aborted {
            echo "Sending message to agent"
        }
        failure {
            echo "Sending message to agent"
        }
        success {
            echo "Sending message to agent"
        }
    }
}