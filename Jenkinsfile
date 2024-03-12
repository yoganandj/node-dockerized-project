pipeline{
    agent any
    stages{
        stage("Build Info"){
            steps{
                script{
                    wrap([$class: 'BuildUser']) {
                        bat 'echo "${BUILD_USER}"'
                        env.VERSION="${env.TIMESTAMP}-${env.GIT_COMMIT.take(7)}"
                        currentBuild.displayName= "${env.BUILD_DISPLAY_NAME} by ${BUILD_USER}"
                        currentBuild.description= "Commit : ${env.GIT_COMMIT.take(7)}, Branch: ${env.GIT_BRANCH}, By: ${BUILD_USER}"
                    }
                }
            }
        }
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
                bat 'docker login -u yogananddocker -p itsmedh@123'
                bat 'docker tag my-node-app:1.0 yogananddocker/my-node-app:1.0'
                bat 'docker push yogananddocker/my-node-app:1.0'
                bat 'docker logout'
            }
        }
        
    }
}