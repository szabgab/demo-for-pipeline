pipeline {
    agent none
    stages {
        stage('build') {
            agent {
                dockerfile {
                    args '-v /var/lib/jenkins/store/demo-for-pipeline/:/store'
                }
            }
            steps {
                echo 'test'
                sh 'python3 --version'
                sh 'pip3 install -r requirements.txt'
                sh 'pytest --junitxml=/store/test-results/$BUILD_NUMBER.xml'
            }
        }
    }
}
