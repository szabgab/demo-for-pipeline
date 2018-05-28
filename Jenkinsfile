pipeline {
    agent none
    stages {
        stage('build') {
            agent {
                docker {
                    image 'python'
                    args '-u root:sudo'
                }
            }
            steps {
                // sh 'uptime'
                sh 'id'
                sh 'uname -a'
                sh '/usr/bin/python --version'
                sh 'pip install -r requirements.txt'
                sh 'rm -rf .pytest_cache/'
                sh 'rm -rf __pycache__/'
                sh 'rm -rf tests/__pycache__/'
                sh 'rm -f *.pyc'
                sh 'pytest --junitxml=test-results/$BUILD_NUMBER.xml'
                // sh 'chown -R jenkins.jenkins test-results'
            }
        }
        stage('release') {
            agent any
            steps {
                sh 'id'
                sh 'DATE=`date "+%Y-%m-%d--%H-%M-%S"`'
                sh 'echo $DATE'
                sh 'tar czf release-$DATE-$GIT_COMMIT.gz demo.py templates/'
            }
        }
    }
    post {
        always {
          node('awesome_node_label') {
            sh 'id'
            archiveArtifacts artifacts: '*.gz'
            junit 'test-results/*.xml'
          }
        }
        cleanup {
          node('awesome_node_label') {
            sh 'id'
            sh 'rm -rf .pytest_cache/'
            sh 'rm -rf __pycache__/'
            sh 'rm -rf tests/__pycache__/'
            sh 'rm -f *.pyc'
          }
        }
    }
}
