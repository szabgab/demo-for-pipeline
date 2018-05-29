pipeline {
    agent none
    stages {
        stage('build') {
            agent { dockerfile true }
            steps {
                echo 'test'
                sh 'python3 --version'
                //sh 'pip install -r requirements.txt'
            }
        }
    }
}
