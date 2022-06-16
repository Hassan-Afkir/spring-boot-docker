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
                withAWS(credentials:registryCredential) {
                    script {
                        sh("/usr/local/bin/aws ecs update-service --cluster hello --service hello2 --force-new-deployment");
                    }

                }
            }
        }
    }
}