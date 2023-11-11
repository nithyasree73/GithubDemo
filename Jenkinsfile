pipeline {
    agent any


    stages{
        stage('Build'){
            steps{
                echo "Build Stage"
            }
        }
        stage('Test'){
            steps{
                 echo "Test Stage"
            }
        }
        stage('Deploy'){
            steps{
                echo "Deploy Stage"
            }
        }
        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'multibranch-sonar-scanner'
            }
            steps {
                script {
                    withSonarQubeEnv('multibranch-sonarqube-server') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        echo "SonarQube analysis failed with status: ${qg.status}"
                        // Add any additional steps or cleanup here
                    } else {
                        echo "SonarQube analysis passed successfully"
                    }
                }
            }
        }
    }
}
