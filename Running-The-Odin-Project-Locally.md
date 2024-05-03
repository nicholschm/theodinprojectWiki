# Running TOP Locally

This page assumes that you have already forked and cloned [The Odin Project](https://github.com/TheOdinProject/theodinproject) (TOP) repo. If you have not, follow the instructions for [setting up a local clone](https://github.com/TheOdinProject/.github/blob/main/CONTRIBUTING.md#setting-up-your-local-clone) from our contributing guide before continuing.

## Table of Contents

* [Initial Installations](#initial-installations)
* [Set Up DotEnv](#set-up-dotenv)
* [Instal Gems and Migrate the Database](#install-gems-and-migrate-the-database)
* [Install JavaScript Modules](#install-javascript-modules)
* [Create the Database](#create-the-database)
* [Get a GitHub API Token](#get-a-github-api-token)
* [Run the Tests](#run-the-tests)
* [Seed the Database and Populate the Lesson Content](#seed-the-database-and-populate-the-lesson-content)
* [Start the Server](#start-the-server)
* [Optional Steps](#optional-steps)
    * [Github OAuth](#github-oauth)
    * [Google OAuth](#google-oauth)

## Initial Installations

* Install Ruby by following the instructions in our [Installing Ruby](https://www.theodinproject.com/lessons/ruby-installing-ruby) lesson.
* Install Rails by following steps 1.1 and 1.2 in [your first Rails app](https://www.theodinproject.com/lessons/ruby-on-rails-installing-rails#your-first-rails-app) from our Installing Rails project.
* Follow the instructions from one of the following operating system specific guides:
    * [Linux Installation Guide](https://github.com/TheOdinProject/theodinproject/wiki/Linux-Installation-Guide)
    * [Mac Installation Guide](https://github.com/TheOdinProject/theodinproject/wiki/OSX-Installation-Guide)

## Set Up DotEnv

TOP uses the [dotenv](https://github.com/bkeepers/dotenv) gem to manage secrets. We will need to make a copy of the `env.sample` file (name it `.env`) and add all our secrets to the new file.

```bash
$ cp env.sample .env
```

Then edit the newly created `.env` file to include your Postgres Username and Password.

```yaml
#------------------------#
# DATABASE CONFIGURATION #
#------------------------#
POSTGRES_USERNAME: 'your-username'
POSTGRES_PASSWORD: 'your-password-here'
```

## Install Gems and Migrate the Database

Next, install the project's gems:

```
$ bundle install
```

**Note: If you are using **Postgres.App**, you may encounter an error installing the `pg` gem. This is likely due to a PATH issue where your pg_config is unable to be found. If you receive an error stating that this gem was not installed, you will need to run the following.**

```bash
find /Applications -name pg_config
```

Then save the path it returns, and then run:

```bash
gem install pg -- --with-pg-config=YOUR_PATH_HERE
```

**Note: If `bundle install` doesn't work and you get a "rbenv version" error of some kind, try running the following command to set your Ruby version in the project.**

```bash
rbenv local 3.3.0
```

**Note: If `bundle install` fails due to “An error occurred while installing sassc (2.4.0), and Bundler cannot continue", follow these instructions to install sassc:**

```bash
$ sudo apt install g++
$ gem install sassc
```

Then retry executing `bundle install`.


## Install JavaScript Modules 

These JavaScript modules (npm packages) are required by [Webpacker](https://github.com/rails/webpacker):

```
$ yarn install
```

**Note: If you get an error about yarn and are on a flavor of Ubuntu, follow the steps outlined in [how to install yarn on Ubuntu](https://linuxize.com/post/how-to-install-yarn-on-ubuntu-20-04/) to install yarn on your machine. Once that's done, run the command Rails suggests and try re-running the above commands.**

## Create the Database

When bundle and yarn have finished installing everything, it's time to get the TOP database set up. To create the database and load the schema:

```
$ rails db:create
$ rails db:environment:set RAILS_ENV=development
$ rails db:schema:load
```

## Get a Github API Token

You will need a Github API Token when running TOP locally to update the curriculum. Without the token you will encouter rate-limiting errors and won't be able to create all the lessons.

You can obtain an API Token by going to [personal access tokens](https://github.com/settings/tokens) in your Github user account settings and click the "generate new token" button. This will bring you to a new page. Give your token a description in the box provided, Something like "Odin " will do. Once that is done click the "generate token" button at the bottom of the page. The token highlighted in green is your new Github API token.

Copy your Github API token and edit your `.env` file with the content below, making sure to paste your API token in place of `<your api token here>`. Note that the `APP_ID` and `SECRET` are commented out. These are used in production and are not needed locally.

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

**Note: If you get an error stating `Cliver::Dependency::NotFound` and `Could not find an executable` and don't have Google Chrome installed, try installing Chrome.**

**Note: If ALL of your tests fail, check to make sure `bundle install` completed without error. You may need to allocate more space to your partition.**

## Seed the Database and Populate the Lesson Content

Next you need to seed the database with the course and lesson data:

```
$ rails db:seed
```

We pull in the lesson content from the Odin [curriculum repository](https://github.com/TheOdinProject/curriculum) on Github. We have created a rake task to do this easily:

```bash
$ rails curriculum:update_content
```

## Start the Server
First install foreman:
```bash
$ gem install foreman
```

You can now run the app on your local machine. First, start the server:

```bash
$ foreman start
```

Then visit [http://localhost:3000](http://localhost:3000) to view TOP in your browser!

**Note: If you encounter an error "You are connecting to Redis 6.0.16, Sidekiq requires Redis 6.2.0 or greater" when executing `foreman start`, you can ensure Redis is up to date by:**

```bash
$ sudo add-apt-repository ppa:redislabs/redis, enter to continue
$ sudo apt-get update
$ sudo apt-get install redis
```

Then check your version with the following code to ensure it is up to date:

```bash
$ redis-server -v
```

## Optional Steps

### Github OAuth
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

### Google OAuth

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
1. Go to `.env` in your local project directory for The Odin Project and fill in the following:
    ```
    GOOGLE_CLIENT_ID: <your client ID here>
    GOOGLE_CLIENT_SECRET: <your client secret here>
    ```
To test all this is working correctly, run the app locally and try to sign up with Google.

## Need Help with Anything Here?
If you run into any problems with the above instructions or have suggestions on how to improve them, please let us know by [creating an issue](https://github.com/TheOdinProject/theodinproject/issues).