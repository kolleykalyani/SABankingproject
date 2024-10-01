pipeline {
    agent any

    stages {
        stage('Build Project') {
            steps {
                git url: 'https://github.com/kolleykalyani/SABankingproject/', branch: 'master'
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t kalyanikolley/staragileprojectfinance:v6 .'
                    sh 'docker images'
                }
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push kalyanikolley/staragileprojectfinance:v6'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'sudo docker run -itd --name container2 -p 8099:8081 kalyanikolley/staragileprojectfinance:v6'
            }
        }
    }
}
