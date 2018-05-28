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
                    args '-u root:sudo -v /var/lib/jenkins/store/demo-for-pipeline/:/store'
                }
            }
            steps {
                sh 'echo build'
                sh 'ln -s /var/lib/jenkins/store/demo-for-pipeline/test-results'
                sh 'touch test-results/1.xml'
                sh 'id'
                sh 'uname -a'
                sh '/usr/bin/python --version'
                sh 'cat /proc/1/cgroup'
                sh 'ls -al'
                sh 'pwd'
                sh 'ls -al trd'
            }
            post {
                always {
                    sh 'echo always after build'
                    sh 'id'
                    sh 'uname -a'
                    sh 'ls -al'
                    sh 'cat /proc/1/cgroup'
                }
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
                sh 'ls -al'
                sh 'id'
                sh 'uname -a'
                sh '/usr/bin/python --version'
                sh 'cat /proc/1/cgroup'
            }
            post {
                always {
                    sh 'echo always after test'
                    sh 'ls -al'
                    sh 'id'
                    sh 'uname -a'
                    sh 'cat /proc/1/cgroup'
                }
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
