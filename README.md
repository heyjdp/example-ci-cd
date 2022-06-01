# example-ci-cd
Just a test repo, used an example of how to CI/CD with GitHub

Tutorial code from https://flask.palletsprojects.com/en/2.1.x/tutorial/ 

## Setup Dev

Do this:

```bash
$ python3 -m venv venv
$ . venv/bin/activate
$ venv/bin/python3 -m pip install --upgrade pip setuptools wheel
$ pip install -r requirements.txt
$ export FLASK_APP=flaskr
$ export FLASK_ENV=development
$ flask init-db
$ flask run
```

Lint:

```bash
$ pip install -r requirements.txt
$ flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
$ flake8 . --count --exit-zero --max-complexity=10 --statistics
```

Test:

```bash
$ pip install -r requirements.txt
$ export FLASK_APP=flaskr
$ export FLASK_ENV=development
$ flask init-db
$ pytest
```

## The Prod(-ish) Commands

NOTE: **THIS IS NOT SUPPOSED TO BE A PROD SERVER, IT IS TEST CODE**

This is the demo code roll-out order of operations:

```bash
$ git clone git@github.com:heyjdp/example-ci-cd.git
$ cd example-ci-cd
$ python3 -m venv venv
$ . venv/bin/activate
$ venv/bin/python3 -m pip install --upgrade pip setuptools wheel
$ pip install -r requirements.txt
$ export FLASK_APP=flaskr
$ flask init-db
$ waitress-serve --call 'flaskr:create_app'
```

To unwind it, if you stood it up in `localhost`:

```bash
$ rm instance/flaskr.sqlite 
$ deactivate
```
