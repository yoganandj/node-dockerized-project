pipeline{
    agent any
    stages{
        stage("checkout"){
            steps{
                checkout scm
            }
        }
        stage("Test"){
            steps{
                bat 'npm install'
                bat 'npm test'
            }
        }
        stage("Build"){
            steps{
                bat 'npm run build'
            }
        }
        stage("Build Image"){
            steps{
                bat 'docker build -t my-node-app:1.0 .'
            }
        }
        stage("Docker Push"){
            steps{
                withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'yogananddocker')]) {
                    bat 'docker login -u yogananddocker -p itsmedh@123'
                    bat 'docker tag my-node-app:1.0 yogananddocker/my-node-app:1.0'
                    bat 'docker push yogananddocker/my-node-app:1.0'
                    bat 'docker logout'
                }
            }
        }
    }
}