# Minimal Django Project Template

My attempt at creating the most bare-bones Django project possible, that is still ready to deploy to a Dokku server

* Basic Django installation project with 1 app, 'main'
* Runs on sqlite built in database
* Includes URL config and routes for at least 1 viewable page (index.html)
* Static assets directories


Start with these comands on a *nix based system with the appropriate requirements:

```
$ mkdir my-new-django-project && cd $_
$ pipenv --python 3
$ pipenv shell
$ pipenv install Django
```

This template can be used locally or remote:

Local use syntax:
```
django-admin startproject --template ~/project-name new_django_project .
```

Remote use syntax:
```
django-admin startproject --template https://github.com/username/repo/archive/master.zip --name=Procfile new_django_project .
```

When the project is ready to deploy, use the following steps to deploy to a server running Dokku:

```
git remote add dokku dokku@your_dokku_fqdn:django-project-name
```

TODO:
- Instruction for Pipfile.log and or requirements.txt
- set up static files properly
- remove node from buildpacks, or add node to project (for deploy error)
- adjust Procfile to work properly / add note to remove || remove it

