**This guide assumes that you have already installed Ruby and rails. To get instructions on how to do that go through the installations project [here](http://www.theodinproject.com/web-development-101/installations)**

## Set up Postgres
Skip this if you have already installed and setup a user for postgresql.

If you're running Ubuntu, postgresql packages are aready in the apt repositories:
```
$ sudo apt-get update
$ sudo apt-get install postgresql postgresql-contrib libpq-dev
```

If not, you'll need to add the postgres repo to your sources and install:
```
$ sudo sh -c "echo 'deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main' > /etc/apt/sources.list.d/pgdg.list"
$ wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | sudo apt-key add -
$ sudo apt-get update
$ sudo apt-get install postgresql-common
$ sudo apt-get install postgresql-9.3 libpq-dev
```

Make sure the postgres server is running
```
sudo systemctl start postgresql

# additionally, to enable postgres at system startup
sudo systemctl enable postgresql
```
Next we need to create our role. Run the following:
```
$ sudo -u postgres createuser yourusername -s
$ sudo -i -u postgres psql
```

```
# Check that the user was created with:
postgres=# \du
# If you want to add a password to the role you created, run:
postgres=# \password yourusername
# Type \q to quit
```
If you encounter an error, `could not connect to server` or `PG::ConnectionBad`, try to start the PG server again:
```
$ sudo systemctl restart postgresql
```

## Installing Gems and Migrating the Database
Now we need to pull down TOP's repository. To do this, go ahead and `fork` [TOP](https://github.com/TheOdinProject/theodinproject.git) repository. In your terminal run:
```
$ git clone https://github.com/YOUR_USERNAME_HERE/theodinproject.git
# Once git finishes cloning, cd into the project directory with
$ cd theodinproject
```

With all that taken care of, install all the gems with `bundle`. Everything should be green:
```
$ bundle install
```

Once bundle finishes, go to `config/database.yml` and write your username and password (only if you added a password) of postgresql for the default section. Next we create and migrate the database:
```
$ rake db:create
$ rake db:migrate
```

Set up the test database:
```
$ rake db:test:prepare
```

## Get a Github API Token
You will need a Github API token to get all the tests to pass and for getting all the lesson content.

First create a application.yml with figaro, this is where you will store your Github API token.
```
$ bundle exec figaro install
```

Next go to [personal access tokens](https://github.com/settings/tokens) in your Github user account settings and click the "generate new token" button. This will bring you to a new page. Give your token a description in the box provided, Something like "Odin " will do. Once that is done click the "generate token" button at the bottom of the page. The token highlighted in green is your new Github API token.

Copy your Github API token and go back to the `config/application.yml` file in your local Odin Project directory. Paste your API token in place of `<your api token here>` like the example below:
```
GITHUB_API_TOKEN: <your api token here>
```

This Github API Token is used when updating the curriculum. Without it you may encounter rate-limiting errors.

## Get a Mailchimp API Key and List ID

[Mailchimp](https://mailchimp.com/) integration is setup to add newly registered users to a specified mailing list. This is done via the [Mailchimp API](https://developer.mailchimp.com/) and gem [Gibbon](https://github.com/amro/gibbon). In order to enable this functionality in your local development and test environments you'll need to:

- Create a [Mailchimp account](https://login.mailchimp.com/signup/)
- Get a Mailchimp [API key](https://kb.mailchimp.com/integrations/api-integrations/about-api-keys)
- Create a [list](https://developer.mailchimp.com/documentation/mailchimp/reference/lists/) to which development/test members will be added
- Get the [list ID](https://kb.mailchimp.com/lists/manage-contacts/find-your-list-id)

Finally, you need to add the API key and list ID to your `config/application.yml`:

```yaml
default: &default
  MAILCHIMP_API_KEY: <your api key here>
  MAILCHIMP_LIST_ID: <your list id here>

development:
  <<: *default

test:
  <<: *default
```


## Run the Tests
You can now run all the tests, they should all be green.

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
```
$ rake curriculum:update_content
```

## Running the app locally
You can now run the app on your local machine.

Start the server
`$ rails server`

Go to the app in your browser:
`http://localhost:3000`

When your local machine reboots, you will have to restart the PG server by running:
`sudo service postgresql start`

## Setting up Github Omniauth (Optional)
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

Go to `config/application.yml` in your local project directory for The Odin Project and fill in the following:
```
GITHUB_API_TOKEN: <your api token here>
GITHUB_APP_ID: <your client ID here>
GITHUB_SECRET: <your client secret here>
```

To test all this is working correctly, run the app locally and try to sign up with Github.

## Need Help?
If you have any problems getting anything set up in this guide please let us know in our [contributing gitter channel](https://gitter.im/TheOdinProject/Contributing).