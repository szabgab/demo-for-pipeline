pipeline {
    agent {
        docker {
            image 'python'
        }
    }
    stages {
        stage('build') {
            steps {
                sh 'uptime'
                sh 'uname -a'
                sh '/usr/bin/python --version'
                sh 'sudo pip install -r requirements.txt'
            }
        }
    }
}
