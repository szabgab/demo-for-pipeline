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
                sh 'sudo apt-get install python3'
                //sh 'python3 --version'
                //sh 'pip install -r requirements.txt'
            }
        }
    }
}
