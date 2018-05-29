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
                //sh 'ln -s /store/test-results'
                //sh 'ln -s /store/artifacts'
                sh 'ls -al'
                //sh 'ls -al test-results/'
                sh 'id'
                sh 'uname -a'
                sh '/usr/bin/python --version'
                sh 'pip install -r requirements.txt'
                sh 'pytest --junitxml=/store/test-results/$BUILD_NUMBER.xml'

                sh 'DATE=`date "+%Y-%m-%d--%H-%M-%S"`; tar czf /store/artifacts/release-$DATE-$GIT_COMMIT.gz demo.py templates/'
            }
            post {
                always {
                    sh 'echo always after build'
                    sh 'pwd'
                    sh 'id'
                    sh 'uname -a'
                    sh 'ls -al'
                    //sh 'ls -al test-results/'
                    //junit '/store/test-results/*.xml'
                    sh 'git clean -fdx'
                    sh 'ls -al'
                }
            }
        }
        stage('deploy') {
            agent { label 'master' }
            steps {
                sh 'echo deploy'
                sh 'id'
                sh 'cd /home/gabor/work/demo-for-pipeline'
                sh '/usr/bin/git pull'
                sh 'sudo /usr/sbin/service uwsgi reload'
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
            //sh 'echo WORKSPACE=$WORKSPACE'
            //sh 'rm -rf $WORKSPACE@*'
            //echo("${env.WORKSPACE}")
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
