pipeline {
    agent none
    stages {
        stage('build') {
            agent {
                docker {
                    image 'python'
                    // args '-u root:sudo'
                }
            }
            steps {
                sh 'uptime'
                sh 'id'
                sh 'uname -a'
                sh 'hostname'
                sh '/usr/bin/python --version'
                sh 'cat /proc/1/cgroup'
            }
        }
    }
    post {
        node {
            always {
                sh 'echo always'
                sh 'id'
                sh 'hostname'
                sh 'cat /proc/1/cgroup'
            }
            changed {
                sh 'echo changed'
                sh 'hostname'
                sh 'id'
            }
            cleanup {
                sh 'echo cleanup'
                sh 'hostname'
                sh 'id'
            }
        }
    }
}
