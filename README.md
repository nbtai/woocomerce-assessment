# WooCommerce Development Docker


## Overview

This docker-compose environment allows you to run a matrix of PHP, MySQL, WordPress and WooCommerce configurations, for example:

| PHP | MySQL | WordPress |   WooCommerce   | Multisite |
|:---:|:-----:|:---------:|:---------------:|:---------:|
| 7.0 |       |  nightly  |      latest     |           |

## Requirements

* Docker >= 1.8.3
* Docker Compose

See [Docker.com](https://www.docker.com/products/docker) for more information. You can install Docker directly from [Docker installation page](https://docs.docker.com/engine/installation/)


## Getting started

1. Make a new project folder and clone (or download) the WooCommerce Development Docker repository:
```bash
$ git clone git@github.com:nbtai/woocomerce-assessment.git
```

2. Start the containers (and watch container logs)
```bash
$ docker-compose -f docker-compose.yml up -d
$ docker-compose -f docker-compose.yml logs -f --tail=10
```

4. Go to http://localhost and log into WordPress with the following credentials:
```
user: admin
password: password
```

> The first build may take some time to complete, if you can not access http://localhost try again after 2-5 minutes.


## Configuration

The `.env` file contains the default settings for the docker containers. 

Dummy data is created using the `fixtures.yml` template. 


## Docker management

### Start
```bash
$ docker-compose -f docker-compose.yml up -d
```

### Watch container logs
```bash
$ docker-compose -f docker-compose.yml logs -f --tail=10
```

### Shut down
```bash
$ docker-compose -f docker-compose.yml kill
```

### List active containers
```bash
$ docker ps
```

### Open container bash
```bash
$ docker exec -it <CONTAINER ID or CONTAINER NAME> bash
```

### Purge all docker containers and images
```bash
$ docker system purge -fa
or
$ docker system prune -fa
```

### Purge database and wordpress install
```bash
$ rm -rf .db && rm -rf .html
```
