# OSX Installation Guide

> This guide assumes that you have already installed homebrew and Ruby on Rails.

## Installing Postgresql 
The Odin Project uses PostgreSQL as it's database. You will need to install it if you haven't already via one of the two methods below:

### via Postgres.app:
The easiest way to get up and running with Postgres is to install [Postgres.App](https://postgresapp.com/) - a nifty program wrapper for PostgreSQL. Once downloaded, install the app and run it.

### via Brew:
PostgreSQL is also available via Brew package manager. Before installing postgres make sure that homebrew is up to date.
```
$ brew update
```

First, install PostgreSQL
```
$ brew install postgresql
```

Once installed, we will need to initialize a new database, then start the Postgres daemon.
```
$ initdb /usr/local/var/postgres
$ pg_ctl -D /usr/local/var/postgres start

# Optional - Start Postgres on system boot:
$ brew services start postgresql
```

## Database Setup
With Postgres installed, we can now turn our attention to setting up the database.  We will be logging into the postgres command line to set up a new user.
```
$ psql postgres

postgres=# CREATE USER your-username WITH PASSWORD your-password-here;
postgres=# ALTER ROLE your-username WITH CREATEDB;
postgres=# \q
```
(Be sure to change `your-username` and `your-password-here` with usernames and passwords of your choosing)

With PostgreSQL installed, continue on with the [Running TOP Locally](https://github.com/TheOdinProject/theodinproject/wiki/Running-The-Odin-Project-Locally) instructions