pipeline {
    agent {
        docker {
            image 'python'
            // args '-u root:sudo'
        }
    }
    stages {
        stage('build') {
            steps {
                sh 'uptime'
                sh 'id'
                sh 'uname -a'
                sh 'hostname'
                sh '/usr/bin/python --version'
            }
        }
    }
    post {
        always {
          node('always_node_label') {
            sh 'id'
            sh 'hostname'
          }
        }
        cleanup {
            node('cleanup_node_label') {
                sh 'echo cleanup'
                sh 'hostname'
                sh 'id'
            }
        }
    }
}
