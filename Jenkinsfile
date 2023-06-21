@Library('jenkins_shared_lib') _

pipeline{
    agent any
    stages{
        stage('Git Checkout'){
            steps{
                gitCheckout(
                    branch: "main",
                    url: "https://github.com/prajwal1691/complete-prodcution-e2e-pipeline-new.git"
                )
            }
        }

        stage('Unit Test Maven'){
            steps{
                script{
                    mvnTest()
                }
            }
        }

    }
}
