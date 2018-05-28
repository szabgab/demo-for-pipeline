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
