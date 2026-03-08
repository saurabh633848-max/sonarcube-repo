pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/saurabh633848-max/website11.git',
                   
            }
        }

        stage('Deploy to Nginx') {
            steps {
                sh 'rsync -av --delete ./ /var/www/html/'
            }
        }

    }
}
