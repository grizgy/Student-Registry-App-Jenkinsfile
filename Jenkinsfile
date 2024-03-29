pipeline {
    agent any

    stages {
        stage('NPM install') {
            steps {
                bat 'npm install'
            }
        }


        stage('NPM audit') {
            steps {
                bat 'npm audit'
            }
        }


        stage('Run integration tests') {
                steps {
                    bat 'npm run test'
                }
            }

        stage('Deploy to production') {
                steps {
                    echo 'deploying'
                }
            }
    }
}