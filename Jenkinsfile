pipeline {
    agent { label 'master' }
    stages {
        stage('build') {
            agent {
                docker {
                    image 'python'
                    //args '-u root:sudo'
                }
            }
            steps {
                sh 'echo build'
                sh 'id'
                sh 'uname -a'
                sh '/usr/bin/python --version'
                sh 'cat /proc/1/cgroup'
            }
        }
        stage('test') {
//            agent {
//                docker {
//                    image 'python'
//                    //args '-u root:sudo'
//                }
//            }
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
