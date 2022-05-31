# example-ci-cd
Just a test repo, used an example of how to CI/CD with GitHub

Tutorial code from https://flask.palletsprojects.com/en/2.1.x/tutorial/ 

## Setup Dev

Do this:

```bash
$ python3 -m venv venv
$ . venv/bin/activate
$ venv/bin/python3 -m pip install --upgrade pip
$ pip install flask
$ export FLASK_APP=flaskr
$ export FLASK_ENV=development
$ flask init-db
$ flask run
```

Test:

```bash
$ pip install pytest coverage
$ export FLASK_APP=flaskr
$ export FLASK_ENV=development
$ flask init-db
$ pytest
```

## The Prod(-ish) Commands

NOTE: **THIS IS NOT SUPPOSED TO BE A PROD SERVER, IT IS TEST CODE**

This is the demo code roll-out order of operations:

```bash
$ git@github.com:heyjdp/example-ci-cd.git
$ cd example-ci-cd
$ python3 -m venv venv
$ . venv/bin/activate
$ venv/bin/python3 -m pip install --upgrade pip
$ pip install flask pytest coverage waitress
$ export FLASK_APP=flaskr
$ flask init-db
$ waitress-serve --call 'flaskr:create_app'
```

To unwind it, if you stood it up in `localhost`:

```bash
$ rm instance/flaskr.sqlite 
$ deactivate
```
