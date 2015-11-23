# Development Environment

# Introduction

This development environment eliminates the need for more than one dependency (e.g. PostgresQL, RVM, Ruby, etc) and leaves you with a single dependency to run all the Civil Service digital applicaion namely Docker.

The repo is a simplified version of the [discovery development environment](https://github.com/crossgovernmentservices/dev-env-discovery)


# Steps

## 1. Install dependencies

- [Docker toolbox](https://www.docker.com/docker-toolbox)


## 2. Clone this repository

**Mac users, note that you must clone this somewhere in your home directory for the default /Users mount in Virtual Box to work.**

    git clone git@github.com:crossgovernmentservices/dev-env.git

## 3. Bootstrap

Run bootstrap script to pull dependencies

    cd dev-env
    ./script/bootstrap

## 4. Start the apps

    # from dev-env directory
    docker-compose build
    docker-compose up

Then see the section below about NGINX proxy

# Adding another application to the development environment

The boostrap script checks out the repos listed in the [config/apps](./config/apps) file. Therefore to add another application, add an entry in config/apps and run bootstrap again.

If the application added needs to be accesible from a browser then add an entry for it into [nginx/nginx.conf](./nginx/nginx.conf). This requires a rebuild of that container. For the moment the easiest thing to do is run:

```
docker-compose build --no-cache
```

# Deleting an image and its containers

This is especially useful when an app's' dependencies change and the image requires a rebuild.

Run the script without arguments to see options, e.g.:

    ./script/docker-delete

# NGINX proxy

The development environment comes an nginx proxy built-in listening on port 80.

To use friendly urls in your browser while running the dev-env application you can set up names pointing to the IP of the VM running the applications. To find out the IP run the following command:

```
docker-machine ip dev-env
``

Use IP address in your /etc/hosts file. For example:

```
192.168.99.102 csdigital.local www.csdigital.local performance.csdigital.local
```

