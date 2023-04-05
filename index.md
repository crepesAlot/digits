![](doc/landing.png)

## Installation

First, [install Meteor](https://www.meteor.com/install).

Second, download a copy of the repository. Please note that you will need to request permission, as the repository is private.

Third, cd into the app/ directory of your local copy of the repo, and install third party libraries with:

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
<br>
  
#### Landing page

When you retrieve the app at http://localhost:3000, this is what should be displayed:

![](doc/landing.png)

The next step is to use the Login menu to either Login to an existing account or register a new account.

#### Login page

Clicking on the Login link, then on the Sign In menu item displays this page:

![](doc/sign-in.png)

#### Register page

Alternatively, clicking on the Login link, then on the Sign Up menu item displays this page:

![](doc/register.png)


#### Landing (after Login) page, non-Admin user

Once you log in (either to an existing account or by creating a new one), the navbar changes as follows:

![](doc/landing-after-login.png)

You can now add new Contacts, and view the Contacts you have added. Note you cannot see any Contacts created by other users.

#### Add Contact page

After logging in, here is the page that allows you to add new Contacts:

![](doc/add-contact.png)

#### List Contacts page

After logging in, here is the page that allows you to list all the Contacts you have added:

![](doc/list-contact.png)

You click the "Edit" link to go to the Edit Contacts page, shown next.

#### Edit Contacts page

After clicking on the "Edit" link associated with an item, this page displays that allows you to change and save it:

![](doc/edit-contact.png)

#### Landing (after Login), Admin user

You can define an "admin" user in the settings.json file. This user, after logging in, gets a special entry in the navbar:

![](doc/admin-landing.png)

#### Admin page (list all users stuff)

To provide a simple example of a "super power" for Admin users, the Admin page lists all of the Contacts by all of the users:

![](doc/admin-list-contact.png)

Note that non-admin users cannot get to this page, even if they type in the URL by hand.
