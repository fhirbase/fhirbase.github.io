---
layout: default
title:  "Heroku"
id: heroku
order: 4
---

1.  Register on [Heroku](https://heroku.com).
2.  Please ensure that you have Ruby installed.
3.  Run this from your terminal:

    ~~~bash
    wget -qO- https://toolbelt.heroku.com/install-ubuntu.sh | sh
    ~~~

4.  Then login and create app

    ~~~sh
    heroku login
    heroku apps:create <your-app-name>
    ~~~

5.  Create PostgreSQL 9.4 database.

    ~~~sh
    heroku addons:add heroku-postgresql --app your-app-name --version=9.4
    ~~~

6.  Find YOUR-DB-NAME at https://postgres.heroku.com/databases. Then restore fhirbase dump and generate tables.

    ~~~sh
    curl https://raw.githubusercontent.com/fhirbase/fhirbase-build/master/fhirbase.sql \
      | pg:psql --app your-app-name YOUR-DB-NAME
    heroku pg:psql --app your-app-name YOUR-DB-NAME --command 'SELECT fhir.generate_tables()'
    ~~~
