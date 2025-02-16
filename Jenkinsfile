pipeline{
    agent{
        label 'Jenkins-agent'
    }
    tools{
        jdk 'Java17'
        maven 'Maven3'
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
        
    }
}
