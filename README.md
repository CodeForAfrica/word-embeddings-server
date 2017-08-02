Media Cloud Word Embeddings Server
==================================

A micro-service to support analyzing words based on models of word embeddings (aka. "word2vec").

Dev Installation
----------------

 * python 2.7 https://www.python.org/download/releases/2.7/
 * `pip install virtualenv` (if necessary) [also install/link pip if you don't have it (if on Mac OS, use sudo easy_install pip)]
 * [`virtualenv venv`](https://virtualenv.pypa.io/en/stable/)
 * activate your virtualenv (and not run any global python installations)
   * on OSX: `source venv/bin/activate`
   * on Windows: `call venv\Scripts\activate`
 * run `pip install -r requirements.txt` to install dependencies
 * run `python download-google-news-model.py` to download the google news model file
 
Developing
----------

We develop [with PyCharm](https://www.jetbrains.com/pycharm/).

Running
-------

Two options:
 1. Development: run `python run.py` to test it out  
 2. Production-like: run `./run.sh` to run it with gunicorn

You can test that with something like this:

```python
import requests
response = requests.post("http://localhost:8000/embeddings/2d.json",
                        data = {'words[]':['one', 'two', 'three'],
                                'model':'GoogleNews-vectors-negative300.bin'})
print response.json()
```

Deploying
---------

This is configured to deploy as a Heroku buildpack to [dokku](http://dokku.viewdocs.io/dokku/).
