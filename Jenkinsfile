pipeline{
    agent{
        label 'Jenkins-agent'
    }
    tools{
        jdk 'Java17'
        maven 'Maven3'
    }
    environment{
        APP_NAME= 'register-app-pipeline'
        RELEASE='1.0.0'
        DOCKER_USER='nithin8'
        DOCKER_PASS='dockerhub'
        IMAGE_NAME='${DOCKER_USER}'+'/'+'${APP_NAME}'
        IMAGE_TAG='${RELEASE}-${BUILD_NUMBER}'
    }
    stages{
        stage('Cleanup workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from SCM'){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/Nithin-kasturi/register-app.git'
            }
        }
        stage('Build applicationn'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Test Applicatoin'){
            steps{
                sh 'mvn test'
            }
        }
        stage("Docker build and push"){
            steps{
            docker.withRegistry('',DOCKER_PASS){
                docker_image=docker.build "${IMAGE_NAME}"
            }
            docker.withRegistry('',DOCKER_PASS){
                docker_image.push("${IMAGE_TAG}")
                docker_image.push('latest')
            }
        }
            
        }
        
    }
}
