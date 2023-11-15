# SWENG-Main-Project

Trello Board 
https://trello.com/invite/b/JzYBrrIW/ATTI9d8d7bbfa462b537c084dbc08148842b2CD9369B/sweng3main

## Explanation of the project structure
Each indivual python file defines what it does at the start of the file. Everyone that edits said file should change the author section to include themselves as the project goes on.

The majority of the webapp is housed within the "/app" directory. Within this directory, the three subdirectories "/auth", "/errors", and "/main" contain flask blueprints for the main features of the app. Auth handles the authentication of users, errors handles all error handling and exceptions within the site, and main contains the main functionality of the app.

The file "models.py" handles the database layout and structure of the webapp. When this is migrated and turned into a database, that database is __currently__ housed locally in the file "app.db".

The folder "/app/templates" contains all html files needed for the project. These html files use bootstrap as a template, as can be seen in "base.html". They are also organised into folders based on flask blueprints, except for all html files used by the main blueprint.

"babel.cfg" is a configuration file for flask-babel, and allows for the translation of all text within the webapp, if that is desired.

"UserTest.py" needs to be moved inside of the "/Testing" folder in the future, but as of now encounters errors when that is attempted, and so is currently at project root.

## Running the app locally
### (Recommended) Run a virtual environment
It is recommended that you do all development with python inside of a virtual environment. 
Due to the large amount of packages and installs needed by this project, a virtual environment prevents any issues of overlapping dependencies from occuring.

As long as you have python installed, you should also have the ability to start a virtual environment. The commands for that are as follows:
* Create a virtual environment:
	`python -m venv venv`
* Activate your new virtual environment (Windows)
	`venv\Scripts\activate`
* Activate your new virtual environment (Not Windows)
	`source venv/bin/activate`
### Install all requirements
Before you can run the app, you must make sure that all required libraries are also installed in your environment. To do this, make sure that you have pulled the file "requirements.txt", and in the same directory as it, run the command:
    `pip install -r requirements.txt`
    
As you work on the project, you may find yourself adding additional installs. To add these to "requirements.txt", run the command:
    `pip freeze > requirements.txt`

### Starting the app
Once all requirements are installed, to start the application run the command:
    `flask run`
    
If you are not using the library flask-dotenv, and/or do not have a the file ".flaskenv", you also need to run the commands telling flask to import the webapp. These are

* Tell Flask how to import the webapp (Windows)
	`set FLASK_APP=webapp.py`
* Tell Flask how to import the webapp (Not Windows)
	`export FLASK_APP=webapp.py`
	
To start the app in debug mode, which uses the inbuilt flask debugger, run the following command (using "set" instead of "export" if on a windows machine.)
    `export FLASK_ENV=development`

### Running Flask as a shell locally
If you want to run flask as a shell locally, with all imports handled, run the following command: `flask shell`

## Using the Database
During the course of the project, new items or relations between items will need to be added to the database. To do this, after adding an object to "models.py", run one of the following commands.

* Create the migration repository for the webapp. You only need to run this if no database has been created yet.
	`flask db init`
* Generate migration script for changes to database. Run this after any update to the database structure.
	`flask db migrate -m [changes name as string]`
	for example: `flask db migrate -m "users table"`
* Apply changes generated by migration script. Run after generating said migration script with the command above.
	`flask db upgrade`
* Undo the latest database migration (useful during development if database migration creates errors)
	`flask db downgrade`

## Localisation and Internationalisation

### Marking text for translation within code
Part of the functioality of the webapp is that it can include translations of text. To mark text that is within the code, and needs translation, put the text in a "_()". An example of a code block from "app/main/models.py" showing this is below.

``` python
from flask_babel import _
...
submit = SubmitField(_l('Submit'))
```

### Translation commands
The following commands are defined within "main/cli.py" and are useable to provide translation functionality and the ability to quickly and easily update the .po and .pot files within the project.

* Add a new language to the project
	`flask translate init [LANG]`
* Update all language repositiries
	`flask translate update`
* Compile all language repositories
	`flask translate compile`

## Emails
The app is currently configured to send emails using local environment variables defined within "config.py". However, these environemnt variables are not defined anywhere. For testing, you should set them locally on your machine. An email will only be sent if the app is not currently in debug mode, and if these variables are set. To set each of them for a **Gmail Email Address**, use the following commands:

*	`export MAIL_SERVER=smtp.googlemail.com`
*	`export MAIL_PORT=587`
*	`export MAIL_USE_TLS=1`
*	`export MAIL_USERNAME=<your-gmail-username>`
*	`export MAIL_PASSWORD=<your-gmail-password>`

These commands will not work if you are not using Gmail. If you are using a windows machine, replace the word "export" above with "set" for setting environment variables.

## Resources used to create this program
A large amount of the base code of this webapp came from this [online web tutorial](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world). However, while this code was used to build the base of the app, as the project progressed it overall was altered into something completely different than what said tutorial initially covers.
