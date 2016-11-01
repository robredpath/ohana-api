# Running Ohana API on your computer

## Overview

The best way to install Ohana API on your own computer will depend on your 

## Obtain the code

If you're looking to deploy the code from this repo quickly, you can just clone it and proceed with installation:

git clone git@github.com:codeforamerica/ohana-api.git && cd ohana-api

We welcome contributions from the community, so we recommend that if you're going to be usig Ohana in the long term, that you [fork this repository to your GitHub account][fork] before you proceed. 

[fork]: http://help.github.com/fork-a-repo/

## Installation

If you're running Windows, we recommend [using Docker](#docker-setup) to get Ohana up and running.

If you're running Linux or macOS, we recommend [using Docker](#docker-setup), but it's also possible to [perform a local installation](#local-installation), especially if you're not familiar with Docker.  

## Docker Setup

1. Download, install, and launch [Docker]

1. Set up the Docker image:

        $ script/bootstrap

1. Start the app:

        $ docker-compose up

Once the docker images are up and running, the app will be accessible at
[http://localhost:8080](http://localhost:8080).

### Verify the app is returning JSON

[http://localhost:8080/api/locations](http://localhost:8080/api/locations)

[http://localhost:8080/api/search?keyword=food](http://localhost:8080/api/search?keyword=food)

We recommend the [JSONView][jsonview] Google Chrome extension for formatting
the JSON response so it is easier to read in the browser.

[jsonview]: https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc

### More useful Docker commands

* Stop this running container: `docker-compose stop`
* Stop and delete the containers: `docker-compose down`
* Open a shell in the web container: `docker-compose run --rm web bash`

[Docker]: https://docs.docker.com/engine/installation/

## Local Setup

Before you can run Ohana API, you'll need to have the following software
packages installed on your computer: Git, PhantomJS, Postgres, Ruby 2.3+,
and RVM (or rbenv).
If you're on a Linux machine, you'll also need Node.js and `libpq-dev`.

If you don't already have all the prerequisites installed, there are two ways
you can install them:

- If you're on a Mac, the easiest way to install all the tools is to use
@monfresh's [laptop] script.

- Install everything manually: [Build tools], [Ruby with RVM], [PhantomJS],
[Postgres], and [Node.js][node] (Linux only).

[laptop]: https://github.com/monfresh/laptop
[Build tools]: https://github.com/codeforamerica/howto/blob/master/Build-Tools.md
[Ruby with RVM]: https://github.com/codeforamerica/howto/blob/master/Ruby.md
[PhantomJS]: https://github.com/jonleighton/poltergeist#installing-phantomjs
[Postgres]: https://github.com/codeforamerica/howto/blob/master/PostgreSQL.md
[node]: https://github.com/codeforamerica/howto/blob/master/Node.js.md

### PostgreSQL Accounts

On Linux, PostgreSQL authentication can be [set to _Trust_](http://www.postgresql.org/docs/9.1/static/auth-methods.html#AUTH-TRUST) [in `pg_hba.conf`](https://wiki.postgresql.org/wiki/Client_Authentication) for ease of installation. Create a user that can create new databases, whose name matches the logged-in user account:

    $ sudo -u postgres createuser --createdb --no-superuser --no-createrole `whoami`

On a Mac with Postgres.app or a Homebrew Postgres installation, this setup is
provided by default.

### Install the dependencies and populate the database with sample data:

    bin/setup

_Note: Installation and preparation can take several minutes to complete!_

### Run the app

Start the app locally on port 8080:

    puma -p 8080

### Verify the app is returning JSON

[http://localhost:8080/api/locations](http://localhost:8080/api/locations)

[http://localhost:8080/api/search?keyword=food](http://localhost:8080/api/search?keyword=food)

We recommend the [JSONView][jsonview] Google Chrome extension for formatting
the JSON response so it is easier to read in the browser.

[jsonview]: https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc

### Configure your instance

That's it! You can now [configure your Ohana API instance](SETUP.md) to meet your own needs
