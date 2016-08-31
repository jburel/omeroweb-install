[![Build Status](https://travis-ci.org/aleksandra-tarkowska/omeroweb-install.svg?branch=master)](https://travis-ci.org/aleksandra-tarkowska/omeroweb-install)


OMERO.web installation scripts
==============================

Example of OMERO.web installation scripts for Linux: Centos7, Ubuntu and Mac OS X.
These scripts are provided to help new users with installing OMERO.web for the
first time on a clean system, and can be used as the basis for more advanced
configurations.

Read the OMERO System Administrator Documentation https://www.openmicroscopy.org/site/support/omero5.3-staging/sysadmins/index.html,
especially the sections on requirements and installation, before using these scripts.

The Linux and OS X scripts should automatically download all required files.


Prerequisites
-------------

    pip install ansible


Building
--------

    ansible-playbook ./ansible/omeroweb-install.yml -i ./ansible/hosts/centos7-ice3.6

to clean up existing scripts:

    ansible-playbook ./ansible/omeroweb-install.yml -i ./ansible/hosts/centos7-ice3.6 --extra-vars "clean=true"

Scripts are autogenerated using ansible, that means they can build directly on the remote host.
Modify `ansible/hosts` and define list of hosts.::

create your own copy of `ansible/hosts/centos7-ice3.6` and define a list of hosts

    ansible-playbook ./ansible/omeroweb-install.yml -i /path/to/hosts/centos7-ice3.6 -u bob

Please note that IcePy 3.5 has to be instlled from RPM, this result in generating
virtualenv with --system-site-packages

Extra vars arguments:

| ARG                | default | optional                | example                  |
|--------------------|---------|-------------------------|--------------------------|
| omero-version      | latest  |                         | OMERO-DEV-breaking-build |
| web-port           | 80      |                         | 8080                     |
| web-prefix         |         |                         | /omero                   |
| web-server-name    |         |                         | omero.example.com        |
| web-server-config  | nginx   | nginx|nginx-development |                          |
| web-session        | False   | True|False              |                          |
| clean              | False   | True|False              |                          |


Running
-------

Environment variables:

| VAR            | default | optional                | example                  |
|----------------|---------|-------------------------|--------------------------|
| OMEROVER       | latest  |                         | OMERO-DEV-breaking-build |
| WEBPORT        | 80      |                         | 8080                     |
| WEBPREFIX      |         |                         | /omero                   |
| WEBSERVER_NAME |         |                         | omero.example.com        |
| WEBSERVER_CONF | nginx   | nginx|nginx-development |                          |
| WEBSESSION     | False   | True|False              |                          |


and run

on Mac OS X::

    ./omeroweb-install-osx-ice3.6
    ./osx/run

on Ubuntu::

    ./omeroweb-install-ubuntu-ice3.6
    ./ubuntu/run

on Centos 7::

    ./omeroweb-install-centos7-ice3.6

or

    ./omeroweb-install-centos7-ice3.5

To run installation scripts on a remote host:

    $ ssh bob@hostname
    $ mv centos7-ice3.6 omeroweb-install-centos7-ice3.6 /tmp/
    $ sudo /tmp/omeroweb-install-centos7-ice3.6  ## absolute path is required


Testing in DOCKER
-----------------


for OS [centos7, ubuntu]::

    ./test/docker-build.sh
    ./test/test_services.sh 

Unfortunately no docker container for Mac OS X

Copyright
---------

2016, The Open Microscopy Environment