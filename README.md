# php-cli-docker

A docker container running PHP 7.0 or PHP 5.6 command line tools.

This container let you run PHP-cli scripts and use much more tools such as Capistrano, GruntJS, Gulp, Bower, Mysql client, etc.

It is design to be run as a daemon and then, let you execute a bash shell. In this shell you will be able to use all tools you need to commit your code, compile assets, deploy, etc.

## Requirements

* docker >= 1.7 [Docker Installation](https://gist.github.com/seblegall/13a663ff73c718b4a58a4cc454fc786c)
* seblegall/php-docker [Php base container](https://github.com/seblegall/php-docker)

## Usage

Pull the container :
```sh
docker pull seblegall/php-cli-docker
```

Run php-cli-docker as a daemon :
```sh
docker run --name="php-cli" -d seblegall/php-cli-docker
```

Exec bash :
```sh
docker exec -it php-cli /bin/bash
```

## Features
Depending on tag you use (e.g. 7.0 or 5.6), this container contains useful tools.

#### Assets Management
* NodeJS
* GruntJS (grunt-cli)
* Gulp
* PhantomJS

#### Database connection
* Mysql client
* PostgresSQL client

#### Editing tools
* Vim
* Emacs

#### Server connection
* Ssh
* Ftp

#### Versionning
* Git

#### Deploy tools
* Capistrano (capistrano-composer, capistrano-symfony)
* Ant

#### Process Management
* Supervisord

## Customization

Edit your git config by modifying the `config/.gitconfig` file.

Edit bash aliases by modifying the `condig/./bash_aliases` file.

## Automatic Building

This container is automatically build with hub.docker.com on git push.

[Docker Hub Repo](https://hub.docker.com/r/seblegall/php-cli-docker/)

## Manual Building

To build the container (replace _<tag>_ by the new container tag e.g. : 5.6):

```sh
docker build -t seblegall/php-cli-docker:<tag> <php_version>/
```

To push the container on hub.docker.com

```sh
docker push seblegall/php-cli-docker:<tag>
```
