pipeline {
    agent { label 'master' }
    stages {
        stage('setup') {
            steps {
                sh 'echo setup'
                sh 'id'
                sh 'uname -a'
                sh 'ln -s /var/lib/jenkins/store/demo-for-pipeline/test-results'
                sh 'ls -al'
            }
        }
        stage('build') {
            agent {
                docker {
                    image 'python'
                    args '-u root:sudo -v /var/lib/jenkins/store/demo-for-pipeline/:/trd'
                }
            }
            steps {
                sh 'echo build'
                sh 'id'
                sh 'uname -a'
                sh '/usr/bin/python --version'
                sh 'cat /proc/1/cgroup'
                sh 'ls -al'
                sh 'pwd'
                sh 'ls -al trd'
            }
        }
        stage('test') {
            agent {
                docker {
                    image 'python'
                    args '-u root:sudo'
                }
            }
            steps {
                sh 'echo test'
                sh 'id'
                sh 'uname -a'
                sh '/usr/bin/python --version'
                sh 'cat /proc/1/cgroup'
            }
        }
    }
    post {
        always {
            sh 'echo always'
            sh 'id'
            sh 'uname -a'
            sh 'cat /proc/1/cgroup'
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
