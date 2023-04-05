![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/landing.png)

meteor-application-template-react is a sample Meteor 2.9 application that illustrates: 

  * A standard directory layout using 'imports/' as recommended in the [Meteor Guide](https://guide.meteor.com/structure.html)
  * [Bootstrap 5 React](https://react-bootstrap.github.io/) for user interface.
  * [Uniforms](https://uniforms.tools/) for form development.
  * [alanning:roles](https://github.com/alanning/meteor-roles) to implement a special "Admin" user.
  * Authorization, authentication, and registration using built-in Meteor packages.
  * Initialization of users and data from a settings file.
  * Alerts regarding success or failure of DB updates using [Sweet Alert](https://sweetalert.js.org/).
  * Quality assurance using [ESLint](http://eslint.org) with packages to partially enforce the [Meteor Coding Standards](https://guide.meteor.com/code-style.html) and the [AirBnB Javascript Style Guide](https://github.com/airbnb/javascript).

The goal of this template is to help you get quickly started doing Meteor development by providing a reasonable directory structure for development and deployment, a set of common extensions to the core framework, and boilerplate code to implement basic page display, navigation, forms, roles, and collection manipulation.

To keep this codebase simple and small, some important capabilities are intentionally excluded from this template:

  * Unit Testing.
  * Security (meteor-application-template-react enables the insecure packages)
  * Deployment

Examples of the these capabilities will be provided elsewhere.

## Installation

First, [install Meteor](https://www.meteor.com/install).

Second, go to [https://github.com/ics-software-engineering/meteor-application-template-react](https://github.com/ics-software-engineering/meteor-application-template-react), and click the "Use this template" button. Complete the dialog box to create a new repository that you own that is initialized with this template's files.

Third, go to your newly created repository, and click the "Clone or download" button to download your new GitHub repo to your local file system.  Using [GitHub Desktop](https://desktop.github.com/) is a great choice if you use MacOS or Windows.

Fourth, cd into the app/ directory of your local copy of the repo, and install third party libraries with:

```
$ meteor npm install
```

## Running the system

Once the libraries are installed, you can run the application by invoking the "start" script in the [package.json file](https://github.com/ics-software-engineering/meteor-application-template-react/blob/master/app/package.json):

```
$ meteor npm run start
```

The first time you run the app, it will create some default users and data. Here is the output:

```
 meteor npm run start 

> meteor-application-template-react@ start /Users/carletonmoore/GitHub/ICS314/meteor-application-template-react/app
> meteor --no-release-check --exclude-archs web.browser.legacy,web.cordova --settings ../config/settings.development.json

[[[[[ ~/GitHub/ICS314/meteor-application-template-react/app ]]]]]

=> Started proxy.                             
=> Started HMR server.                        
=> Started MongoDB.                           
I20230404-22:35:09.512(-10)? Creating the default user(s)
I20230404-22:35:09.518(-10)?   Creating user admin@foo.com.
I20230404-22:35:09.587(-10)?   Creating user john@foo.com.
I20230404-22:35:09.650(-10)? Creating default contacts.
I20230404-22:35:09.650(-10)?   Adding: Johnson (john@foo.com)
I20230404-22:35:09.676(-10)?   Adding: Casanova (john@foo.com)
I20230404-22:35:09.677(-10)?   Adding: Binsted (admin@foo.com)
=> Started your app.

=> App running at: http://localhost:3000/
```

Periodically, you might see `Error starting Mongo (2 tries left): Cannot run replSetReconfig because the node is currently updating its configuration` after the `=> Started HMR server.`. It doesn't seem to be a problem since the MongoDB does start.

### Viewing the running app

If all goes well, the template application will appear at [http://localhost:3000](http://localhost:3000).  You can login using the credentials in [settings.development.json](https://github.com/ics-software-engineering/meteor-application-template-react/blob/main/config/settings.development.json), or else register a new account.

### ESLint

You can verify that the code obeys our coding standards by running ESLint over the code in the imports/ directory with:

```
meteor npm run lint
```

## Walkthrough

The following sections describe the major features of this template.

### Directory structure

The top-level directory structure is:

```
.github     # holds the GitHub Continuous Integration action and Issue template.
app/        # holds the Meteor application sources
config/     # holds configuration files, such as settings.development.json
doc/        # holds developer documentation, user guides, etc.
.gitignore  # don't commit IntelliJ project files, node_modules, and settings.production.json
```

This structure separates documentation files (such as screenshots) and configuration files (such as the settings files) from the actual Meteor application.

The app/ directory has this structure:

```
.deploy/
  .gitignore     # don't commit mup.js or settings.json
  mup.sample.js  # sample mup.js file used for deploying the application
  settings.sample.json # sample settings file
  
client/
  main.html      # The boilerplate HTML with a "root" div to be manipulated by React.
  main.js        # import startup files.

imports/
  api/           # Define collections
    contact/       # The Contacts collection definition
    note/          # The Notes collection definition
  startup/       # Define code to run when system starts up (client-only, server-only, both)
    client/
    server/
  ui/
    components/  # Contains page elements, some of which could appear on multiple pages.
    layouts/     # Contains top-level layout (<App> component).
    pages/       # Contains components for each page.

node_modules/    # managed by npm

public/          # static assets (like images) can go here.

server/
   main.js       # import the server-side js files.
   
tests/           # testcafe acceptance tests.
```

### Import conventions

This system adheres to the Meteor guideline of putting all application code in the imports/ directory, and using client/main.js and server/main.js to import the code appropriate for the client and server in an appropriate order.

### Application functionality

The application implements a simple CRUD application for managing "Contact", which is a Mongo Collection consisting of a firstName (String), a lastName (String), a condition (one of 'excellent', 'good', 'fair', or 'poor') and an owner.

By default, each user only sees the Contacts that they have added.  However, the settings file enables you to define default accounts.  If you define a user with the role "admin", then that user gets access to a special page which lists all the contacts defined by all users.

#### Landing page

When you retrieve the app at http://localhost:3000, this is what should be displayed:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/landing.png)

The next step is to use the Login menu to either Login to an existing account or register a new account.

#### Login page

Clicking on the Login link, then on the Sign In menu item displays this page:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/sign-in.png)

#### Register page

Alternatively, clicking on the Login link, then on the Sign Up menu item displays this page:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/register.png)


#### Landing (after Login) page, non-Admin user

Once you log in (either to an existing account or by creating a new one), the navbar changes as follows:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/landing-after-login.png)

You can now add new Contacts, and view the Contacts you have added. Note you cannot see any Contacts created by other users.

#### Add Contact page

After logging in, here is the page that allows you to add new Contacts:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/add-contact.png)

#### List Contacts page

After logging in, here is the page that allows you to list all the Contacts you have added:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/list-contact.png)

You click the "Edit" link to go to the Edit Contacts page, shown next.

#### Edit Contacts page

After clicking on the "Edit" link associated with an item, this page displays that allows you to change and save it:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/edit-contact.png)

#### Landing (after Login), Admin user

You can define an "admin" user in the settings.json file. This user, after logging in, gets a special entry in the navbar:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/admin-landing.png)

#### Admin page (list all users stuff)

To provide a simple example of a "super power" for Admin users, the Admin page lists all of the Contacts by all of the users:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/admin-list-contact.png)

Note that non-admin users cannot get to this page, even if they type in the URL by hand.

### Collections

The application implements a single Collection called "Contacts". Each Contacts document has the following fields: firstName, lastName, address, image, description, and username.

The Contacts collection is defined in [imports/api/stuff/stuff.js](https://github.com/ics-software-engineering/meteor-application-template-react/blob/main/app/imports/api/stuff/stuff.js).

The Contacts collection is initialized in [imports/startup/server/Mongo.js](https://github.com/ics-software-engineering/meteor-application-template-react/blob/main/app/imports/startup/server/Mongo.js).
