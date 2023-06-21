@Library('jenkins_shared_lib') _

pipeline{
    agent any
    parameters{
        choice(name: 'action', choices: 'create\ndelete', description: 'choose create/Destroy')
    }
    stages{
        when { expression { param.action == 'create' }}
        stage('Git Checkout'){
            steps{
                gitCheckout(
                    branch: "main",
                    url: "https://github.com/prajwal1691/complete-prodcution-e2e-pipeline-new.git"
                )
            }
        }

        stage('Unit Test Maven'){
            when { expression { param.action == 'create' }}
            steps{
                script{
                    mvnTest()
                }
            }
        }

        stage('Maven Integration Test'){
            when { expression { param.action == 'create' }}
            steps{
                script{
                    mvnIntegrationTest()
                }
            }
        }

        stage('Static Code Analysis: Sonarqube'){
            when { expression { param.action == 'create' }}
            steps{
                script{
                    statiCodeAnalysis()
                }
            }
        }

    }
}
