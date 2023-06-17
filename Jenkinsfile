pipeline{
    agent{
        label "jenkins-agent"
    }
    tools{
        jdk 'Java17'
        maven 'Maven3'
    }
    stages{
        stage('clean up workspace'){
            steps{
                cleanWs()
            }
        }
    
        stage('checkout scm'){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/prajwal1691/complete-prodcution-e2e-pipeline-new'
            }
        }

        stage('Build Application'){
            steps{
                sh "mvn clean package"
            }
        }

        stage('Test Application'){
            steps{
                sh "mvn test"
            }
        }

        stage('Sonarqube Analysis'){
            steps{
                withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token') {
                   sh "mvn sonar:sonar"
                }
            }
        }
    }
}
