---
layout: default
title:  "Local"
id: local
order: 1
---

Requirements

* PostgreSQL 9.4
* pgcrypto
* pg_trgm
* btree_gin
* btree_gist

Installation steps:

```bash
sudo apt-get install postgresql-9.4 postgresql-contrib-9.4 curl
# create local user for ident auth
sudo su postgres -c 'createuser -s <you-local-user>'
# create empty database
psql -d postgres -c 'create database test'
# install last version of fhirbase
curl https://raw.githubusercontent.com/fhirbase/fhirbase-build/master/fhirbase.sql | psql -d test
# generate tables
psql -d test -c 'SELECT fhir.generate_tables()'

psql test
#> \dt
```
<a href="#" class="btn btn-default btn-lg" id="download">Download</a>


Here is asci cast for the simplest installation - [https://asciinema.org/a/17236].
