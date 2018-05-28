pipeline {
    agent { label 'master' }
    stages {
        stage('build') {
            agent {
                docker {
                    image 'python'
                    args '-u root:sudo -v /var/lib/jenkins/store/demo-for-pipeline/:/store'
                }
            }
            steps {
                sh 'echo build'
                sh 'ln -s /store/test-results'
                sh 'ls -al'
                sh 'ls -al test-results/'
                sh 'id'
                sh 'uname -a'
                sh '/usr/bin/python --version'
                sh 'pip install -r requirements.txt'
                sh 'pytest --junitxml=test-results/$BUILD_NUMBER.xml'
            }
            post {
                always {
                    sh 'echo always after build'
                    sh 'id'
                    sh 'uname -a'
                    sh 'ls -al'
                    sh 'ls -al test-results/'
                    junit './test-results/*.xml'
                    sh 'git clean -fdx'
                    sh 'ls -al'
                }
            }
        }
    }
    post {
        always {
            sh 'echo always'
            sh 'id'
            sh 'uname -a'
        }
        changed {
            sh 'echo changed'
            sh 'id'
            sh 'uname -a'
        }
        cleanup {
            sh 'echo cleanup'
            sh 'id'
            sh 'uname -a'
        }
    }
}
