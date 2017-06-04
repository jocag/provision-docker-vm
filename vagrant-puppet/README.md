[![Build Status](https://travis-ci.org/jocag/provision-docker-vm.svg?branch=master)](https://travis-ci.org/jocag/provision-docker-vm)  [![Docker Automated build](https://img.shields.io/badge/docker%20build-automated-blue.svg)](https://hub.docker.com/r/jocag/vagrant-puppet/)

# Puppet Base Image
## Summary
This repository contains a dockerised [Puppet](https://github.com/puppetlabs/puppet) installation published to the public [Docker Hub](https://hub.docker.com/r/jocag/vagrant-puppet/) registry using automated builds in [Docker Cloud](https://cloud.docker.com/app/jocag/repository/docker/jocag/vagrant-puppet/general)

The Dockerfile for this image can be found in this Github repository [provision-docker-vm](https://github.com/jocag/provision-docker-vm)

## How to Obtain This Image
You can simply pull this image from [Docker Hub](https://hub.docker.com/r/jocag/vagrant-puppet) using one of the available tags.

`$docker pull jocag/vagrant-puppet:centos`

## Building Your Own Container Based on an Image (Optional)
To build this image, simply pull this repository and cd into the directory that contains your preferred Dockerfile and run:  

`$docker build -t vagrant-puppet:latest .`

## Configuration
There are base images available currently for CentOs 7.x and Ubuntu 16.04 systems, using both a Puppet stable version and Puppet agent 1.8.3.

Also, you can choose what Puppet version you would like to run:
- Puppet 3
  - puppet3_ubuntu
  - puppet3_centos


- Puppet 4
  - puppet4_ubuntu
  - puppet4_centos

If you are required to use a newer agent version, you can update the Puppet agent currently installed in the Docker image updating the variable `PUPPET_AGENT_VERSION`

`ENV PUPPET_AGENT_VERSION="1.8.3"`

Then, you must rebuild the base image as explained in the [Building Your Container](#Building Your Own Container Based on an Image) section.

## Usage
Although, you can run a Docker container using this image straight after pulling from Docker Hub running:  

```
docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro jocag/vagrant-puppet:centos
```

You might prefer using the Vagrantfile included. It can be placed into your remote/local repository and can be run using Docker as its default provider.

This new Vagrant VM generated can be used to code and test Puppet modules and manifests on different OS running locally inside a container.

Also, it will build the necessary docker image if you did not pull it beforehand.

`$vagrant up dummy_box`

## License
This software is shipped under the MIT License. Feel free to copy, modify or add extra software for your own purposes.  
Forks and Pull requests are welcome!
