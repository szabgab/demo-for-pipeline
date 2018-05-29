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
                sh 'pwd'
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
                    sh 'pwd'
                    sh 'id'
                    sh 'uname -a'
                    sh 'ls -al'
                    sh 'ls -al test-results/'
                    //junit 'test-results/*.xml'
                    sh 'git clean -fdx'
                    sh 'ls -al'
                }
            }
        }
        stage('release') {
            agent any
            steps {
                sh 'id'
                sh 'DATE=`date "+%Y-%m-%d--%H-%M-%S"`'
                sh 'echo $DATE'
                sh 'ln -s /store/artifacts'
                sh 'ls -al'
                sh 'tar czf artifacts/release-$DATE-$GIT_COMMIT.gz demo.py templates/'
            }
        }
    }
    post {
        always {
            sh 'echo always'
            sh 'pwd'
            sh 'id'
            sh 'ls -la'
            sh 'uname -a'
        }
        changed {
            sh 'echo changed'
            sh 'pwd'
            sh 'id'
            sh 'uname -a'
        }
        cleanup {
            sh 'echo cleanup'
            sh 'pwd'
            sh 'id'
            sh 'uname -a'
            pwd()
            sh 'echo WORKSPACE=$WORKSPACE'
            echo("${env.WORKSPACE}")
            dir("${env.WORKSPACE}@2") {
                deleteDir()
            }
            dir("${env.WORKSPACE}@2@tmp") {
                deleteDir()
            }
            dir("${env.WORKSPACE}@tmp") {
                deleteDir()
            }
        }
    }
}
