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
                sh 'dotnet publish ./app/*.csproj -c Release -o ./publish'

            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-dotnet-app:latest ./app'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh 'ansible-playbook playbook.yml'
            }
        }
    }
}
