pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/salman1256/my-dotnet-app.git'
            }
        }

        stage('Build & Publish .NET App') {
            steps {
                // Publish .NET binaries to publish/ folder
                sh 'dotnet publish app.csproj -c Release -o ./publish'
            }
        }

        stage('Prepare Docker Context') {
            steps {
                // Copy Dockerfile and playbook.yml into publish directory
                sh 'cp Dockerfile ./publish/'
                sh 'cp playbook.yml ./publish/'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-dotnet-app:latest ./publish'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                // Run Ansible from workspace root (not inside publish)
                sh 'ansible-playbook playbook.yml'
            }
        }
    }
}
