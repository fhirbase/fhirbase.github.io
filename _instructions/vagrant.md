---
layout: default
title:  "Vagrant"
id: vagrant
order: 2
---

The simplest and cross-platform installation can be done using Vagrant.

1. Install [vagrant][] according to its documentation or check you already have it.

[vagrant]: https://www.vagrantup.com/downloads.html

~~~bash
vagrant --version
# Vagrant 1.8.1
~~~

2. Clone Fhirbase project and go to the project folder.

~~~bash
git clone https://github.com/fhirbase/fhirbase-plv8.git fhirbase
cd fhirbase
~~~

3.  Launch vagrant.

This action could take a time to load fhirbase container

~~~bash
vagrant up
~~~

4. Test your Fhirbase installation.

~~~bash
echo "SET plv8.start_proc = 'plv8_init'; SELECT fhirbase_version();" \
    | psql postgres://fhir:fhirbase@127.0.0.1:2345/fhir
~~~

You should see output with version number of the installed Fhirbase.
