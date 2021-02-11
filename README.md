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

### Develop locally
You may find anther way works better - however you can easily use the Pipenv created to create the project like:

```
$ pipenv install -r deploy_template_test/requirements.txt 
```

### Static Files
Static files are pretty confusing. Whitenoise is an external Django library that makes it easier to use 1 server for both hosting Django and static files. Whitenoise requires and installed app and a layer of middleware to work correctly.

The `collectstatic` command should create a staticfiles dir at the root level.


When the project is ready to deploy, use the following steps to deploy to a server running Dokku:

You will need to initiaize the project with git, at some point. If you haven't already:
```
cd /path/to/new_django_project
git init .

# after git init, add remote for dokku server
git remote add dokku dokku@your_dokku_fqdn:django-project-name
```
If you're deploying, add server to ALLOWED_HOSTS, something like:
`- ALLOWED_HOSTS = [*]`
`ALLOWED_HOSTS = ['127.0.0.1','your-fqdv.net']`

Adjust Procfile
The default Procfile needs to be manually set to your project name: 
`- web: gunicorn {{ project_name }}.wsgi --log-file `
`+ web: gunicorn django-project-name.wsgi --log-file `

Do the usual git add / commit stuff after files are changed and ready.

Should be ready to git push!
`git push dokku master`

 TODO:
