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


        stage('Build image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'a388566f-4a99-4c63-bca6-b6339bdd1878', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    bat """docker build -t grizgy/studentapp:1.0.0 .
                        docker login -u %user%--password %pass%
                        docker push grizgy/studentapp:1.0.0"""
                }
            }
        }    


        stage('Deploy to production') {
                steps {
                 script {
                    input("Deploy to production?")
                 }
                 
                withCredentials([usernamePassword(credentialsId: 'a388566f-4a99-4c63-bca6-b6339bdd1878', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    bat """docker pull grizgy/studentapp:1.0.0 .
                        docker run -d -p 8081:8081 grizgy/studentapp:1.0.0"""
                }



                }
            }
    }
}