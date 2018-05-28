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
            }
        }
        stage('testing') {
            steps {
                sh 'pytest --junitxml=test-results/$BUILD_NUMBER.xml'
            }
        }
        stage('release') {
            steps {
                sh 'DATE=`date "+%Y-%m-%d--%H-%M-%S"`'
                sh 'echo $DATE'
                sh 'tar czf release-$DATE-$GIT_COMMIT.gz demo.py templates/'
            }
        }
        stage('deploy') {
            agent { label 'labelName' }
            steps {
                sh 'echo deploy'
                sh 'id'
                sh 'cd /home/gabor/work/demo-for-pipeline'
                sh '/usr/bin/git pull'
                sh 'sudo /usr/sbin/service uwsgi reload'
            }
        }
    }
    post {
        always {
            sh 'id'
            archiveArtifacts artifacts: '*.gz'
            junit 'test-results/*.xml'
            sh 'rm -rf .pytest_cache/'
            sh 'rm -rf __pycache__/'
            sh 'rm -rf tests/__pycache__/'
        }
    }
}
