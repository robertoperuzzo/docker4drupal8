# Docker-based Drupal 8 environment for local development
## Introduction

Docker4Drupal8 is a set of docker containers optimized for Drupal8. 

Use docker-compose.yml file from this repository to spin up local environment on Linux, Mac OS X and Windows. This file is based on [docker4drupal](https://github.com/wodby/docker4drupal) configuration with some changes to work with Drupal 8 projects created using [Drupal Console](https://drupalconsole.com/) and [Drupal Composer](https://github.com/drupal-composer/drupal-project) template.

For more information read [getting started](http://docs.docker4drupal.org/en/latest/).

## Changes
1. Mapping all drupal-compose's directories structure in docker's volumes.

```yml  
  php:
    ...
    volumes:
#      - ./:/var/www/html
      - ./vendor:/var/www/vendor
      - ./drush:/var/www/drush
      - ./scripts:/var/www/scripts
      - docker-sync-unison:/var/www/web # Replace volume to this to use docker-sync for macOS users

  nginx:
    ...
    environment:
      NGINX_BACKEND_HOST: php
      NGINX_SERVER_ROOT: /var/www/web
    volumes:
#      - ./:/var/www/html
      - docker-sync-unison:/var/www/web # Replace volume to this to use docker-sync for macOS users
```

2. Enabled docker-sync configuration for macOS users.

```yml
# Docker-sync for macOS users
volumes:
 docker-sync-unison:
   external: true
```

## Install docker-sync for macOs users
Install docker-sync and its dependencies.

### Docker Sync
Run your application at full speed while syncing your code for development, finally empowering you to utilize Docker for development under OSX.

Go to the [project page](http://docker-sync.io) for more informations.

```
gem install docker-sync
```

### Unison
Unison is a file-synchronization tool for OSX, Unix, and Windows. It allows two replicas of a collection of files and directories to be stored on different hosts (or different disks on the same host), modified separately, and then brought up to date by propagating the changes in each replica to the other.

Go to the [project page](http://www.cis.upenn.edu/~bcpierce) for more informations.

```
brew install unison
```

### Unison fsmonitor for macOS
Go to the [project page](https://github.com/hnsl/unox) for more informations.

```
curl "https://raw.githubusercontent.com/hnsl/unox/master/unox.py" -o "/usr/local/bin/unison-fsmonitor" && chmod +x /usr/local/bin/unison-fsmonitor

sudo easy_install pip && sudo -H pip install watchdog
```

### Mac fsevents
```
sudo easy_install pip && sudo -H pip install macfsevents
```
