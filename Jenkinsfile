pipeline {
    environment {
        registry = '216413260795.dkr.ecr.us-east-2.amazonaws.com/jenkins-pipeline'
        registryCredential = 'sam-jenkins-demo-credentials'
        dockerImage = ''
    }
    agent {
        
        docker {
            image 'maven:3.8.1-adoptopenjdk-11' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    stages {
        
        stage('Deploy EC2') {
            steps {
                withCredentials([string(credentialsId: 'AWS_REPOSITORY_URL_SECRET', variable: 'AWS_ECR_URL')]) {
                
                    script {
                        sh "aws ecs update-service --cluster hello --service hello2 --force-new-deployment";
                    }

                }
            }
        }
    }
}