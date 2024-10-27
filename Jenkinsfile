pipeline {
    agent any
    stages {
        stage('checkout the code from github') {
            steps {
                git url: 'https://github.com/kolleykalyani/Banking-java-project/'
                echo 'github url checkout'
            }
        }
        stage('codecompile with kalyani') {
            steps {
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('codetesting with kalyani') {
            steps {
                sh 'mvn test'
            }
        }
        stage('qa with kalyani') {
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('package with kalyani') {
            steps {
                sh 'mvn package'
            }
        }
        stage('deploy with ansible') {
            steps {
                sh 'ansible-playbook ansible-playbook.yml'
            }
        }
        
        stage('port expose') {
            steps {
                sh 'docker run -dt -p 8081:8081 --name c000 myimg'
            }
        }
    }
}
