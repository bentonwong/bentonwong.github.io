---
layout: post
title:      "How to Deploy a Node/Express Application to Heroku"
date:       2017-11-26 22:42:46 +0000
permalink:  how_to_deploy_a_node_express_application_to_heroku
---

Deploying a Node/Express application to Heroku is fairly easy and quick with the following process:
## Requirements

1) A node application

2) A [Heroku](http://www.heroku.com) account

3) Git installed

## Pre-deployment

### 1) Set up dynamic port binding

In development, we would usually specify the listening port in the index.js file such as:

`app.listen(5000);`

Heroku will dynamically assign the application a port to use in production. The node application must be able to change its listening port accordingly.  Therefore, we can do that by making this simple change to allow for this:

```
const PORT = process.env.PORT || 5000;
app.listen(PORT);
```

Then in production, we can get the Heroku generated port number from process.env.PORT and the default port number in development.

### 2) Specify the node environment

```
In the package.json file, insert the following lines to specify the desired node version:
"engines": {
    "node": "x.x.x",
    "npm": "x.x.x"
  },
```

### 3) Specify the start script

In development, we manually start an application by typing into the terminal something like "node index.js".  To have Heroku start the application in production, we add a line into the package.json under scripts:

```
"scripts": {
    "start": "node index.js"
  }
```

Remove the existing line for the test script.

### 4) Create a .gitignore file

Heroku will provide dependencies in production.  When deploying, we do not want to include the one used in development (e.g node_modules folder).

In the root directory, create a file named “.gitignore”.  Then, simply add the string “node_modules” to that file and save the .gitignore file.

This will instruct git not to commit the node_modules folder and its contents.

## Deployment
### 1) Commit codebase to git

From the repo’s directory in its terminal, type ‘git init’.

Type ‘git add . ‘.

Type git commit -m “my commit message”.

### 2) Install Heroku CLI

Instructions to install it are at https://devcenter.heroku.com/articles/heroku-cli#download-and-install.

For users on Mac OS X: type into the terminal: ‘brew install heroku’.

Confirm installation with ‘heroku -v’, which should return the version of Heroku CLI installed.

### 3) Log into Heroku from the terminal

From the terminal type: 'heroku login'.

You will be prompted to enter your heroku account login credentials.  Enter your Heroku credentials here in order to proceed to the next step.

### 4) Create a Heroku app

Create a Heroku app by typing ‘heroku create’ in the terminal.  This should provide urls to the app and the heroku git repository. We will need to refer back to the heroku git repository url in the next step.

### 5) Deploy your app's codebase to Heroku

Before we deploy to Heroku, we must point the app's git remote url on Heroku.

Use the returned git address (e.g. git.heroku.com/<app_name>.git) to set up the repo’s remote Heroku repository by typing in the terminal: ‘git add remote heroku <insert the app’s git address here>’.

Type ‘git remote -v’ to confirm that the repository is pointing to the correct Heroku git remote address.

Finally, we deploy by typing into the terminal: 'git push heroku master'.  This process may take a couple minutes and will provide a confirmation message once the deployment is complete.

## Post-deployment
Check the deployment by inspecting application on Heroku.

1) Type ‘heroku open’ which will open the application in a new browser window.

2) If there are any errors, type ‘heroku logs’ which will provide clues as to the cause of the error(s) and assist in the debugging process.

