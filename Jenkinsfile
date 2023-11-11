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
                    withSonarQubeEnv('multibranch-sonar-server') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                def qg = waitForQualityGate()
                if (qg.status != 'OK') {
                    error "SonarQube analysis failed with status: ${qg.status}"
                }
            }
        }
    }
}
