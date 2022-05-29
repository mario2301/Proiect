pipeline {
    environment {
        registry = "mario2301/p-load_balancer"
        registryCredential = 'dockerhub-cred'
        dockerImage = ''
        dockerFile = 'dockerfile.lb'
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/mario2301/Proiect.git'
            }
        }        
        stage('Building Docker image') {
            steps{
                script {
                    dockerImage = docker.build(registry,"-f ./dockerfiles/${dockerFile} .")
                }
            }
        }
        stage('Push Docker image on DockerHub') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Cleaning up') {
            steps{
                sh "docker rmi $registry"
            }
        }
    }
}