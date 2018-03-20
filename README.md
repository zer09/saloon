# Saloon

[![Build Status](https://travis-ci.org/go-saloon/saloon.svg?branch=master)](https://travis-ci.org/go-saloon/saloon)
[![GoDoc](https://godoc.org/github.com/go-saloon/saloon?status.svg)](https://godoc.org/github.com/go-saloon/saloon)

Saloon is a _Work in Progress_ forum based on [Buffalo](https://gobuffalo.io).

## Database setup

One needs a database to run `saloon`.
Here is an example, running postgres inside a docker container:

```
$> docker run --name saloon-postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres
```

### Create Your Databases

Ok, so you've edited the "database.yml" file and started postgres, now Buffalo can create the databases in that file for you:

```
$> buffalo db create -a
v4.2.0

created database saloon-test
created database saloon-prod
created database saloon-dev
```

You can run `saloon` to initialize the forum and the content of its database:

```
$> saloon migrate
> create_users
> create_categories
> create_topics
> create_replies
> create_forums

0.6591 seconds

$> saloon t db:setup
DEBU[2018-03-20T15:39:44+01:00] INSERT INTO users (admin, avatar, created_at, email, full_name, id, password_hash, subscriptions, updated_at, username) VALUES (:admin, :avatar, :created_at, :email, :full_name, :id, :password_hash, :subscriptions, :updated_at, :username)
DEBU[2018-03-20T15:39:44+01:00] INSERT INTO forums (created_at, description, id, logo, title, updated_at) VALUES (:created_at, :description, :id, :logo, :title, :updated_at)
```

The `db:setup` task created an `admin` user with (by default) a password `admin`.
You change that!

## Starting the Application

Buffalo ships with a command that will watch your application and automatically rebuild the Go binary and any assets for you.
That's useful when developing on `saloon`.
To do that run the "buffalo dev" command:

```
$> buffalo dev
```

If you point your browser to [http://127.0.0.1:3000](http://127.0.0.1:3000) you should see a "Welcome to the Saloon Forum" page.

In production, one can instead directly run the `saloon` executable:

```
$> saloon
INFO[0000] Starting application at 127.0.0.1:3000
INFO[2018-03-20T15:40:31+01:00] Starting Simple Background Worker
[...]
```
