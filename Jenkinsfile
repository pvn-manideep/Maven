pipeline {
    agent any

    tools {
        maven 'Maven'  // Matches the name you’ll configure in Jenkins tools
    }

    stages {
        stage('Checkout Code') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/pvn-manideep/Maven.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'  // Builds your app and creates a JAR file
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Deploy Using Ansible') {
            steps {
                sh 'ansible-playbook -i inventory.ini deploy.yml'
            }
        }
    }
}
