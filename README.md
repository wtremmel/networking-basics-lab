# README #

## What is this repository for? ##

* Lab enviroment running [Wireshark](https://wireshark.org) in Docker containers

## How do I get set up? ##

This has been tested using CentOS7 and Ubuntu. For remote setup there is also an ansible playbook incluced.

You need 500MB RAM per seat. So for 20 Seats, 10GB RAM is recommended.

### Docker ###

You need Docker to run this. Please install:

- Docker Community Edition
    - For Ubuntu: https://docs.docker.com/install/linux/docker-ce/ubuntu/
    - For CentOS: https://docs.docker.com/install/linux/docker-ce/centos/
- Docker-Compose: https://docs.docker.com/compose/install/

It is recommended to use the newest Docker packages from the docker website as packages included in your linux distribution might be outdated.

### Packages needed ###

You need the following packages for your Linux distribution:

* fortune (yes, really, for generating sample texts)
* netcat or nc

### Who do I talk to? ###

* [DE-CIX Academy](https://de-cix.net/academy), academy@de-cix.net
