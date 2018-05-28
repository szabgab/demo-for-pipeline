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

        stage('release') {
            steps {
                sh 'DATE=`date "+%Y-%m-%d--%H-%M-%S"`'
                sh 'echo $DATE'
                sh 'tar czf release-$DATE-$GIT_COMMIT.gz demo.py templates/'
            }
        }
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
        always {
            sh 'id'
            archiveArtifacts artifacts: '*.gz'
            junit 'test-results/*.xml'
        }
    }

