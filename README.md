[![Build Status](https://travis-ci.org/jocag/provision-docker-vm.svg?branch=master)](https://travis-ci.org/jocag/provision-docker-vm) [![Docker Automated build](https://img.shields.io/badge/docker%20build-automated-blue.svg)](https://hub.docker.com/u/jocag)

# Provision Docker VM
A series of Dockerfiles, for building Docker images containing different software configuration management tools.

The aim is to build a Docker image as a Virtualbox replacement for provisioning new Vagrant VMs with Ansible/Puppet.
These new Vagrant VMs generated can be used to code and test Puppet modules/manifests and Ansible playbooks on different OS running locally inside a container.

## Description
These Docker images are intended to be generic and reusable. This repository provides the corresponding Dockerfile and Vagranfile for each image allowing you to add/remove packages or simply use them locally for your own purposes. They were created following current Docker best practices and can be good starting points for custom images.

You can find published versions of these images on [Docker Hub](https://hub.docker.com/u/jocag):

* [![](https://images.microbadger.com/badges/image/jocag/vagrant-puppet.svg)](https://microbadger.com/images/jocag/vagrant-puppet) [vagrant-puppet](https://github.com/jocag/provision-docker-vm/tree/master/vagrant-puppet)  
* [![](https://images.microbadger.com/badges/image/jocag/vagrant-ansible.svg)](https://microbadger.com/images/jocag/vagrant-ansible) [vagrant-ansible](https://github.com/jocag/provision-docker-vm/tree/master/vagrant-ansible)  


## How to Obtain These Images
You can simply pull any of these images from [Docker Hub](https://hub.docker.com/r/jocag) using one of the available tags.

`$docker pull <docker_image>:<tag> .`

e.g.
`$docker pull vagrant-puppet:puppet4_ubuntu .`

## Building Images (Optional)
To build this image, simply pull this repository and you can find the relevant Dockerfile in the directory of the same name.
Then, you only need to run in a terminal:  

`$docker build -t <docker_image>:<tag> .`

e.g.
`$docker build -t vagrant-puppet:latest .`

## Usage
Although, you can run a Docker container using any of these images straight after pulling from Docker Hub running:  

```
docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro jocag/vagrant-puppet:centos
```

You might prefer using the Vagrantfile included. It can be placed into your remote/local repository and can be run using Docker as its default provider.

This new Vagrant VM generated can be used to code and testing on different OS running locally inside a container.

`$vagrant up dummy_box`

NOTE: If you are using a different Vagrantfile, remember specify Docker as your provider when running Vagrant:

`$vagrant up dummy_box --provider=docker`

## Adding Additional Images
If you do find yourself customizing these images, please open pull request and share with the community describing why and whether your use is something that could benefit others people handling these images.

## License
This software is shipped under the MIT License. Feel free to copy, modify or add extra software for your own purposes.  
Forks and Pull requests are welcome!
