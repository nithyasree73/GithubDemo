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
        environment{
            scannerHome = tool 'multibranch-sonar-scanner'
        }

            steps {
            withSonarQubeEnv('multibranch-sonarqube-server') {
                sh "${scannerHome}/bin/sonar-scanner"
            }

        }


}
