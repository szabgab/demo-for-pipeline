pipeline {
    agent none
    stages {
        stage('build') {
            agent { dockerfile true }
            steps {
                echo 'test'
                sh 'python3 --version'
                sh 'pip install -r requirements.txt'
                sh 'pytest' //  --junitxml=/store/test-results/$BUILD_NUMBER.xml'
            }
        }
    }
}
