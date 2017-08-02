Media Cloud Word Embeddings Server
==================================

A micro-service to support analyzing words based on word embeedings (ala word2vec).

Dev Installation
----------------

Python 2.7:
 * python 2.7 https://www.python.org/download/releases/2.7/
 * `pip install virtualenv` (if necessary) [also install/link pip if you don't have it (if on Mac OS, use sudo easy_install pip)]
 * [`virtualenv venv`](https://virtualenv.pypa.io/en/stable/)
 * activate your virtualenv (OSX: `source venv/bin/activate`, Windows: `call venv\Scripts\activate`) to activate your virtual environment (and not run any global python installations)
 * On Window, make sure to create an environment variable: `set NODE_ENV=dev`
 * in MediaMeter directory run `pip install -r requirements.txt` 
 
And you have to download and install the GoogleNews model yourself:
`wget https://github.com/mmihaltz/word2vec-GoogleNews-vectors/blob/master/GoogleNews-vectors-negative300.bin.gz -P ./models/`
 
Developing
----------

We develop [with PyCharm](https://www.jetbrains.com/pycharm/).

Running
-------

Run `python run.py` to test the app out.  Then do something like this to test it out:

```python
import requests
response = requests.post("http://localhost:5000/embeddings/2d.json",
                        data = {'words[]':['one', 'two', 'three'],
                                'model':'GoogleNews-vectors-negative300.bin'})
print response.json()
```

This loads the GoogleNews model on startup, so it will take a minute to load.

Or `./run.sh` to run it with gunicorn in a more production-like way.  You can test that with something like this:

```python
import requests
response = requests.post("http://localhost:8000/embeddings/2d.json",
                        data = {'words[]':['one', 'two', 'three'],
                                'model':'GoogleNews-vectors-negative300.bin'})
print response.json()
```


Deploying
---------

This is configured to deploy with docker.

```
docker run -p 8080:5000 mediacloud/wordembeddings
```
