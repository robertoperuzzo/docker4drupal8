# Docker-based Drupal 8 environment for local development
## Introduction

Docker4Drupal8 is a set of docker containers optimized for Drupal8. 

Use docker-compose.yml file from this repository to spin up local environment on Linux, Mac OS X and Windows. This file is based on [docker4drupal](https://github.com/wodby/docker4drupal) configuration with some changes to work with Drupal 8 projects created using [Drupal Console](https://drupalconsole.com/) and [Drupal Composer](https://github.com/drupal-composer/drupal-project) template.

For more information read [getting started](http://docs.docker4drupal.org/en/latest/).

## Changes
```yml  
  php:
    ...
    volumes:
      - ./web:/var/www/web
      - ./vendor:/var/www/vendor

  nginx:
    ...
    environment:
      NGINX_BACKEND_HOST: php
      NGINX_SERVER_ROOT: /var/www/web/
    volumes:
      - ./web:/var/www/web
      - ./vendor:/var/www/vendor
```
