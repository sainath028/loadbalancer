pipeline {
    agent any

    stages {

        stage('git clone') {
            steps {
                // git branch: 'master', url: "https://github.com/sainath028/vprofile-repo.git"  
                sh "echo git"
            }
        }
        stage('Docker login'){
            steps{
                sh 'aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/e7w1y6p1'
            }
        }
        stage('Docker build') {
            steps{
                sh "docker build -t demo ."
            }
        }        
        
        stage('Docker tag') {
            steps{
                sh "docker tag demo:latest public.ecr.aws/e7w1y6p1/demo:$BUILD_NUMBER"
            }
        }  

        stage('Docker push') {
            steps{
                sh "docker push public.ecr.aws/e7w1y6p1/demo:$BUILD_NUMBER"
            }
        }  
     }
 }
