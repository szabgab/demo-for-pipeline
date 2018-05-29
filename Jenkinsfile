pipeline {
    agent none
    stages {
        stage('build') {
            agent {
                docker {
                    image 'ubuntu:latest'
                }
            }
            steps {
                echo 'test'
                sh 'python3 --version'
                sh 'pip install -r requirements.txt'
            }
        }
    }
}
