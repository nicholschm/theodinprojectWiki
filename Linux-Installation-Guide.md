**This guide assumes that you have already installed Ruby and rails. To get instructions on how to do that go through the installations project [here](https://www.theodinproject.com/lessons/ruby-installing-ruby)**

## Install Redis
We use Redis for our asynchronous background jobs, for example sending emails. To get the app up and running and for all the tests to pass you will need to install Redis.

```
$ sudo apt update
$ sudo apt install redis-server
```

Redis should have started automatically after installing it, to verify run the following:
```
$ sudo systemctl status redis-server
```

You should see something that says Redis is active.

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

# OPTIONAL: start postgres at system startup
sudo systemctl enable postgresql
```
Next we need to create our role. We recommend using your $USER as your postgres username (the one you see when you open a terminal). In moritz@moritz-TECRA-R940:~ the username is moritz.  Run the following:
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

With PostgreSQL installed, continue on with the [Running TOP Locally](https://github.com/TheOdinProject/theodinproject/wiki/Running-The-Odin-Project-Locally) instructions