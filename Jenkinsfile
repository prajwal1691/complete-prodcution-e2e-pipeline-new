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
    }
    stages{
        stage('checkout scm'){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/prajwal1691/complete-prodcution-e2e-pipeline-new'
            }
        }
    }
}
