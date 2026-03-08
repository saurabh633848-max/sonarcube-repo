pipeline {
    agent any

    tools {
        sonarQube 'SonarScanner'  // Make sure this matches the name in Jenkins configuration
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
                withSonarQubeEnv('SonarQube') {  // Name of the SonarQube server in Jenkins
                    sh """
                        sonar-scanner \
                        -Dsonar.projectKey=sonar-repo \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://52.66.205.81:9000 \
                        -Dsonar.login=<your-token>
                    """
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
        always {
            echo "SonarQube analysis complete. Check results here: http://52.66.205.81:9000/dashboard?id=sonar-repo"
        }
    }
}
