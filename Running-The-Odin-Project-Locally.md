# Running TOP Locally

> This page assumes that you have already installed Ruby, Rails and PostgreSQL. Please go back to the [Linux Installation Instructions](https://github.com/TheOdinProject/theodinproject/wiki/Linux-Installation-Guide) or [Mac Installation Instructions](https://github.com/TheOdinProject/theodinproject/wiki/OSX-Installation-Guide) if you haven't already. 

First, make sure you're in the `theodinproject` directory. All instructions should be followed while inside of that directory.
```bash
$ cd theodinproject
```

## Setting up DotEnv
TOP uses the [dotenv](https://github.com/bkeepers/dotenv) gem to manage secrets. We will need to make a copy of the `env.sample` file (name it `.env`) and add all our secrets to the new file.
```bash
$ cp env.sample .env
```

Then edit the `.env` to include your Postgres Username and Password.

```yaml
#------------------------#
# DATABASE CONFIGURATION #
#------------------------#
POSTGRES_USERNAME: 'your-username'
POSTGRES_PASSWORD: 'your-password-here'
```

## Edit database.yml
Type `code config/database.yml` to edit the database.yml file. Go to line 20 and line 21 in the code. It should say
```
test: &test
  <<: *default
```
Replace this code with 
```
test: &test
  <<: *default
  database: 'theodinproject_test'
  username: YOUR_POSTGRES_USERNAME
  password: YOUR_POSTGRES_PASSWORD
```

## Installing Gems and Migrating the Database

Next, install the project's gems:
```
$ bundle install
```

When bundle has finished installing everything, it's time to get the TOP database set up.

Create the databases and migrate them:
```
$ rails db:create
$ rails db:migrate
```

## Get a Github API Token
You will need a Github API Token when running TOP locally to update the curriculum. Without the token you will encouter rate-limiting errors and won't be able to create all the lessons.

You can obtain an API Token by going to [personal access tokens](https://github.com/settings/tokens) in your Github user account settings and click the "generate new token" button. This will bring you to a new page. Give your token a description in the box provided, Something like "Odin " will do. Once that is done click the "generate token" button at the bottom of the page. The token highlighted in green is your new Github API token.

Copy your Github API token and edit your `.env.local` file with the content below, making sure to paste your API token in place of `<your api token here>`. Note that the `APP_ID` and `SECRET` are commented out. These are used in production and are not needed locally.
```
GITHUB_API_TOKEN: <your api token here>
#GITHUB_APP_ID: 1234
#GITHUB_SECRET: 1234
```



## Run the Tests
You can now run all the tests, they should all be green

To run the rspec unit tests:
```
$ rspec
```

## Seeding the Database and Populating the Lesson content
Next you need to seed the database with the course and lesson data.
```
$ rails db:seed
```

We pull in the lesson content from the Odin [curriculum repository](https://github.com/TheOdinProject/curriculum) on Github. We have created a rake task to do this easily.
```bash
$ rails curriculum:update_content
```

## Running the app locally
You can now run the app on your local machine. First, start the server:
```bash
$ rails server
```

and then visit [http://localhost:3000](http://localhost:3000) to view TOP in your browser!

**Note for macOS 10.13 and above:** You may need to run `export OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES` before `rails server`. See [this blog post](https://blog.phusion.nl/2017/10/13/why-ruby-app-servers-break-on-macos-high-sierra-and-what-can-be-done-about-it/) for more information.

## OPTIONAL: Get a Mailchimp API Key and List ID

[Mailchimp](https://mailchimp.com/) integration is setup to add newly registered users to a specified mailing list. This is done via the [Mailchimp API](https://developer.mailchimp.com/) and gem [Gibbon](https://github.com/amro/gibbon). In order to enable this functionality in your local development and test environments you'll need to:

- Create a [Mailchimp account](https://login.mailchimp.com/signup/)
- Get a Mailchimp [API key](https://kb.mailchimp.com/integrations/api-integrations/about-api-keys)
- Create a [list](https://developer.mailchimp.com/documentation/mailchimp/reference/lists/) to which development/test members will be added
- Get the [list ID](https://kb.mailchimp.com/lists/manage-contacts/find-your-list-id)

Finally, you need to add the API key and list ID to your `.env`:

```
MAILCHIMP_API_KEY: <your api key here>
MAILCHIMP_LIST_ID: <your list id here>
```

## OPTIONAL: Github OAuth
We allow users to create an account on the site with Github OAuth. To get this feature working locally follow the instructions in this section.

Go to [OAuth Applications](https://github.com/settings/developers) in your Github user account settings and click the "register a new application" button.

Fill in the form fields with the following:

Application Name
`odin`

Homepage URL
`http://localhost:3000`

Application Description
`the odin project`

Authorization callback URL
`http://localhost:3000/users/auth/github/callback`

Click the "Register application" button. This will display your `Client ID` and `Client Secret` which is what you will use to get OAuth working on your local machine.

Go to `.env` in your local project directory for The Odin Project and fill in the following:
```
GITHUB_API_TOKEN: <your api token here>
GITHUB_APP_ID: <your client ID here>
GITHUB_SECRET: <your client secret here>
```

To test all this is working correctly, run the app locally and try to sign up with Github.


## OPTIONAL: Google OAuth
We also allow users to create an account on the site with Google OAuth. To get this feature working locally follow the instructions in this section.

Visit the [Google API Console](https://console.developers.google.com/) to obtain OAuth credentials and agree to terms of service.

1. Click "Select a Project" drop down
1. Click "New Project" button on top right
    1. Set project name to `odin`
    1. Location can be default `No Organization`
    1. Click "Create" button

1. Click "Credentials" in left nav.
    1. Navigate to "OAuth Consent Screen" on top nav.
        1. Set Application name `odin`
        1. Scroll to bottom and click "Save" button
  1. Click "Create Credentials" drop down
      1. Select "OAuth Client ID"
      1. Select "Web Application" for Application type
      1.  Fill in the form fields with the following:
          1.  Name: `odin`
          1.  Authorized Javascript Origins: `http://localhost:3000` *make sure to press Enter to add it*
          1.  Authorized redirects URIs: `http://localhost:3000/users/auth/google/callback` *make sure to press Enter to add it*
          1.  Click "Create" button. This will display your `Client ID` and `Client Secret` which is what you will use to get OAuth working on your local machine.
1. Go to `.env.local` in your local project directory for The Odin Project and fill in the following:
    ```
    GOOGLE_CLIENT_ID: <your client ID here>
    GOOGLE_CLIENT_SECRET: <your client secret here>
    ```
To test all this is working correctly, run the app locally and try to sign up with Google.

## Need Help?
If you have any problems getting anything set up in this guide please let us know in our [Admin room in Discord](https://discordapp.com/channels/505093832157691914/540903304046182425)