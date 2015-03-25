---
layout: default
title:  "Vagrant"
id: vagrant
order: 2
---

The simplest and cross-platform installation can be done using Vagrant.

1.  Install [vagrant](http://www.vagrantup.com/downloads) according to
    its documentation or check you already have it.

    ~~~bash
    vagrant -v
    # Vagrant 1.7.2
    ~~~

2.  Clone FHIRbase project and go to the project folder.

    ~~~bash
    git clone https://github.com/fhirbase/fhirbase.git
    cd fhirbase
    ~~~

3.  Launch vagrant.

    ~~~bash
    sudo vagrant up
    # this action could take a time to load fhirbase container
    ~~~

4.  Check your ssh-config settings and remember your ip.

    ~~~bash
    vagrant ssh-config
    # HostName 172.17.0.15 <<- vm <ip>
    #  User vagrant
    #  Port 22
    ~~~

5.  Use your <ip> in the next command to connect to the database.

    ~~~bash
    psql -h <ip> -p 5432 -U fhirbase
    # password: fhirbase
    ~~~

6.  If you like GU interfaces use pgadmin with connection

    * host: <ip>
    * database: fhirbase
    * user: fhirbase
    * password: fhirbase
