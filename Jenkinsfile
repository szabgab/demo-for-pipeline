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
                sh 'virtualenv venv'
                sh 'source venv/bin/activate'
                sh 'pip install -r requirements.txt'
            }
        }
    }
}
