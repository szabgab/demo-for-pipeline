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
                sh 'pip install -r requirements.txt'
            }
        }
    }
}
