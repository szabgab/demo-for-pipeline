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
                sh 'rm -f *.pyc'
                sh 'pytest --junitxml=test-results/$BUILD_NUMBER.xml'
            }
        }
    }
    stage('release') {
        steps {
            sh 'id'
            sh 'DATE=`date "+%Y-%m-%d--%H-%M-%S"`'
            sh 'echo $DATE'
            sh 'tar czf release-$DATE-$GIT_COMMIT.gz demo.py templates/'
        }
    }
    post {
        cleanup {
            sh 'id'
            sh 'rm -rf .pytest_cache/'
            sh 'rm -rf __pycache__/'
            sh 'rm -rf tests/__pycache__/'
            sh 'rm -f *.pyc'
        }
    }
}
