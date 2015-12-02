# Heroku & How to deploy applications

Heroku is a cloud hosting platform as a service. That means you do not have to worry about infrastructure; just focus on your application. Additionally:
* Instant Deploy with Git push
* Plenty of Add-on resources (applications, databases etc.)
* Logging and Visibility

## Critical components of deploying a Flask application to Heroku:
* **heroku command line toolkit [heroku toolbet]** (required)

  Provides access to the heroku Command Line Interface (CLI), which is used for publishing (pushing) and managing apps.

* **heroku login** (required)

	Authentication is required to allow heroku commands to operate.

* **python virtual environment** (recommended)

  Creates a safe isolated environment for app development which is robust and independent of operating systems.

* **heroku local test** (recommended)

	Test app locally before deploying to heroku.

* **requirements.txt** (required)

	Contains list of python and flask plugins/libraries to be installed on the heroku server/container. This can also be used for local development.

* **procfile** (required)

	This is like ```app.run``` to explicitly declare what command is executed to run the app on heroku.

* **git**(required)

	Heroku uses git as the default method of publishing apps to its container and to keep track of all changes. GitHub is not a requirement.

* **heroku create** (required)

	Creates an app on heroku, which prepares heroku to receive your app source code. Heroku generates a random name which can be changed from heroku online website dashboard.

* **heroku** push (required)

  The command to deploy the app on heroku. Performs a set of steps like installing python/flask plugins and executing the procfile to bring the app to life. The app url is provided as part of the command line output.

## Nifty commands to manage & troubleshoot heroku app

To execute the following commands, open up command line switch to the app directory, authenticate using ```heroku login``` and then type-in the commands.

* ```heroku ps``` - display app status
* ```heroku open``` - open app in web browser
* ```heroku logs``` - view errors/warnings/alerts about running app
* ```heroku apps``` - display list of apps associate to your account
* ```heroku apps:info``` - display app information like url, repo name etc.
* ```heroku apps:destory --app APPNAME``` - delete app from heroku
* ```heroku help``` - view usage summary of various commands

Additional information:
https://devcenter.heroku.com/articles/using-the-cli

## Deploy a custom application to Heroku - First time

We will use the templates assignment as an example to create and deploy a heroku app. The steps below can be used for deploying any Flask app but should be adapted as required.

Pre-requisites:
* heroku account
* python
* git
* sense of humor

##### Step 1 - Create a folder/directory
This folder can be located anywhere on the system and all commands will be executed from within this directory

##### Step 2 - Download templates source code
Extract zip file into the newly created directory
[Click here to download zip file](https://github.com/SI539/tutorials/raw/master/heroku/flasktemplates.zip)

#### Step 3 - Add ```.gitignore```
Create a file named ```.gitignore``` to exclude additional files and folders before deploying to heroku. Contents of file:
```
venv
*.pyc
```

#### Step 4 - Login to heroku
* Execute: ```heroku login``` and enter credentials

#### Step 5 - Create and activate virtual environment
* Execute: ```virtualenv venv``` (creating virtualenv)
* Execute (mac): ```source venv/bin/activate``` (activating virtualenv)
* Execute (windows): ```venv/bin/activate```(activating virtualenv)

#### Step 6 - Install Python / Flask plugins
* Execute: ```pip install Flask```
* Execute: ```pip install gunicorn```

#### Step 7 - Create procfile
Create a file named **Procfile** (no file extension) and add the following line: ```web: gunicorn app:app --log-file=-```

The first part of the ```app:app``` is to point to the main app.py file. If the main Flask file was ```portfolio.py```, the Procfile would contain the following: ```web: gunicorn portfolio:app --log-file=-```

#### Step 8 - Test if app runs locally
* Execute: ```heroku local```

#### Step 9 - Save installed packeges in requirements file
* Execute: ```pip freeze > requirements.txt```

#### Step 10 - Initialize git repository
* Execute: ```git init```
* Execute: ```git add .```
* Execute: ```git commit -m "first commit"```

#### Step 11 - Deploy app
* Execute: ```heroku create```
* Execute: ```git push heroku master```

#### Step 12 - Visit the app
The web address is displayed while deploying the app as part of the above command. Or execute: ```heroku open```

#### Step 13 (bonue) - Check application logs
* Execute: ```heroku logs```

## Deploy changes to existing heroku application
To avoid repeating the following steps multiple times, it is advised to test by running the app locally through heroku. Use: ```heroku local```. But if the changes are unavoidable and need to be pushed to heroku, follow the steps below:

#### Step 1 - Make changes to the app
Make any changes to the app.py file or the html files

#### Step 2 - Commit changes to git
Heroku looks for git commits (changes) and only then pushes the changes to the remote app server.
* Execute: ```git status``` (to view changes to the application)
* Execute: ```git add .```
* Execute: ```git commit -m "Update author name and routes"``` (this message should be descriptive but concise)

#### Step 3 - Deploy changes to app on heroku
* Execute: ```git push heroku master```

---
#### Additional commands

* Install python plugins automagically (requires requirements.txt file to be present)

	Execute: ```pip install -r requirements.txt```

---
Credits:
https://devcenter.heroku.com/articles/getting-started-with-python-o
