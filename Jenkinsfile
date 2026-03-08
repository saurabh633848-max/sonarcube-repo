pipeline {
    agent any

    environment {
        PROJECT_KEY = 'sonar-repo'
        SONAR_SERVER = 'SonarQube'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/saurabh633848-max/sonarcube-repo.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    // Fetch SonarScanner path from Jenkins tool configuration
                    def scannerHome = tool 'mySonarScanner'

                    withSonarQubeEnv("${SONAR_SERVER}") {
                        sh """
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=${PROJECT_KEY} \
                        -Dsonar.sources=.
                        """
                    }
                }
            }
        }

        stage('Deploy to Nginx') {
            steps {
                sh 'rsync -av --delete ./ /var/www/html/'
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
            echo "SonarQube Report: http://52.66.205.81:9000/dashboard?id=sonar-repo"
        }

        failure {
            echo "Pipeline failed. Check Jenkins logs."
        }

        always {
            echo "Pipeline execution finished."
        }
    }
}
