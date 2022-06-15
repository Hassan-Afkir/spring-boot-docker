pipeline {
    environment {
        registry = '216413260795.dkr.ecr.us-east-2.amazonaws.com/jenkins-pipeline'
        registryCredential = 'jeinkins-aws'
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
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Create image') {
                steps { 
                    script{
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    }
                }
            }
        stage('Deploy image') {
            steps{
                script{
                    docker.withRegistry("https://" + registry, "ecr.us-east-2:" + registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}