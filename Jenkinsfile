@Library('jenkins_shared_lib') _

pipeline{
    agent jenkins-slave01
    parameters{
        choice(name: 'action', choices: 'create\ndelete', description: 'choose create/Destroy')
    }
    stages{
        stage('Git Checkout'){
            when { expression { params.action == 'create' }}
            steps{
                gitCheckout(
                    branch: "main",
                    url: "https://github.com/prajwal1691/complete-prodcution-e2e-pipeline-new.git"
                )
            }
        }

        stage('Unit Test Maven'){
            when { expression { params.action == 'create' }}
            steps{
                script{
                    mvnTest()
                }
            }
        }

        stage('Maven Integration Test'){
            when { expression { params.action == 'create' }}
            steps{
                script{
                    mvnIntegrationTest()
                }
            }
        }

        stage('Static Code Analysis: Sonarqube'){
            when { expression { params.action == 'create' }}
            steps{
                script{
                    def SonarQubecredentialsId = 'sonarqube-api'
                    statiCodeAnalysis(SonarQubecredentialsId)
                }
            }
        }

        stage('Quality Gate Status Check: Sonarqube'){
            when { expression { params.action == 'create' }}
            steps{
                script{
                    def SonarQubecredentialsId = 'sonarqube-api'
                    QualityGateStatus(SonarQubecredentialsId)
                }
            }
        }

        stage('Maven Build: Maven'){
            when { expression { params.action == 'create' }}
            steps{
                script{
                    mvnBuild()
                }
            }
        }

    }
}
