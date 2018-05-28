pipeline {
    agent {
        docker {
            image 'python'
            args '-u root:sudo'
        }
    }
    stages {
        stage('build') {
            steps {
                sh 'uptime'
                sh 'id'
                sh 'uname -a'
                sh '/usr/bin/python --version'
                sh 'pip install -r requirements.txt'
                sh 'rm -rf .pytest_cache/'
                sh 'rm -rf __pycache__/'
                sh 'rm -rf tests/__pycache__/'
                sh 'rm *.pyc'
                sh 'pytest --junitxml=test-results/$BUILD_NUMBER.xml'
            }
        }
    }
}
