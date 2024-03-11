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
                withCredentials([usernamePssword(credentialsId: 'docker_cred', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]){
                    bat 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    bat 'docker tag my-node-app:1.0 yogananddocker/my-node-app:1.0'
                    bat 'docker push yogananddocker/my-node-app:1.0'
                    bat 'docker logout'
                }
                
            }
        }
    }
}