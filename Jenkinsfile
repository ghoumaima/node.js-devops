pipeline {
    agent any
    environment {
        
        DOCKERHUB_CREDENTIALS = credentials('dockerproject')
    }
    stages {
        stage('Checkout'){
            agent any
            steps{
                
                git branch: 'main', url:'https://github.com/ghoumaima/node.js-devops.git'
            }
        }
        stage('Init'){
            steps{
                
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Build'){
            steps {
                
                sh 'docker build -t oumaima5/nodejen-docker-app:$BUILD_ID -f ./Dockerfile .'
                //sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/calculator-app:$BUILD_ID' 
            }
        }
        stage('Deliver'){
            steps {
                
                sh 'docker push oumaima5/nodejen-docker-app:$BUILD_ID'
            }
        }
        stage('Cleanup'){
            steps {
            
            sh 'docker rmi oumaima5/nodejen-docker-app:$BUILD_ID'
            sh 'docker logout'
            }
        }
    }
}