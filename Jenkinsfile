@Library('jenkins_shared_lib') _

pipeline{
    agent {
        label 'jenkins-slave01'
    }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    parameters{
        choice(name: 'action', choices: 'create\ndelete', description: 'choose create/Destroy')
        string(name: 'ImageName', description: 'name of the docker build', defaultValue: 'javaapp')
        string(name: 'ImageTag', description: 'tag of the docker build', defaultValue: 'v1')
        string(name: 'DockerHubUser', description: 'name of the application', defaultValue: 'prajwal1691')
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

        stage('Docker Image Build'){
            when { expression { params.action == 'create' }}
            steps{
                script{
                    dockerBuild("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
                }
            }
        }

        stage('Docker Image Scan'){
            when { expression { params.action == 'create' }}
            steps{
                script{
                    dockerImageScan("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
                }
            }
        }

    }
}
