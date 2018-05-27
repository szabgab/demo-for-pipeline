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
                sh 'python --version'
            }
        }
    }
}
