# Demo application for Jenkins Pipelines

To be used for the Jenkins demo.

http://demo.code-maven.com:9091/


## Development server

```
FLASK_APP=app FLASK_DEBUG=1 flask run --host 0.0.0.0 --port 5000
```

Visit http://127.0.0.1:5000/


## Deployed server

```
cd work
git clone https://github.com/szabgab/demo-for-pipeline.git
cd demo-for-pipeline
virtualenv venv -p python --no-site-packages
source venv/bin/activate
pip install -r requirements.txt
```

```
apt-get install uwsgi  uwsgi-plugin-python
ln -s /home/gabor/work/demo-for-pipeline/uwsgi/demo.ini /etc/uwsgi/apps-enabled/
```


        stage('deploy') {
            agent { label 'labelName' }
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
    }

pipeline {
    agent none
    stages {
        stage('build') {
            agent {
                docker {
                    image 'python'
                    args '-u root:sudo'
                }
            }
            steps {
                // sh 'uptime'
                sh 'id'
                sh 'uname -a'
                sh '/usr/bin/python --version'
                sh 'pip install -r requirements.txt'
                sh 'rm -rf .pytest_cache/'
                sh 'rm -rf __pycache__/'
                sh 'rm -rf tests/__pycache__/'
                sh 'rm -f *.pyc'
                sh 'pytest --junitxml=test-results/$BUILD_NUMBER.xml'
                // sh 'chown -R jenkins.jenkins test-results'
            }
        }
    }
    post {
        always {
          node('awesome_node_label') {
            sh 'id'
            archiveArtifacts artifacts: '*.gz'
            junit 'test-results/*.xml'
          }
        }
        cleanup {
          node('awesome_node_label') {
            sh 'id'
            sh 'rm -rf .pytest_cache/'
            sh 'rm -rf __pycache__/'
            sh 'rm -rf tests/__pycache__/'
            sh 'rm -f *.pyc'
          }
        }
    }
}
