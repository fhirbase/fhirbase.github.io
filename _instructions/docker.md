---
layout: default
title:  "Docker"
id: docker
order: 3
---

1.  You can install FHIRbase using docker. First you have to install [docker](https://www.docker.com/) itself according to provided documentation (see the [installation section](https://docs.docker.com/installation/#installation)).

2.  For this installation we are going to use docker-containers - images, which are stored in the Docker Hub repository or can be built manually. Depending on your goals you can get different docker images:

    * Stable versioned tagged build [fhirbase-build](https://registry.hub.docker.com/u/fhirbase/fhirbase-build). Select
      the desired tag from tags, for example 0.0.9-alpha4, and run the
      following command:

      ~~~bash
      sudo docker run --name=fhirbase -p 5433:5432 -d fhirbase/fhirbase-build:0.0.9-alpha4
      ~~~

    * The latest automatically deployed on commit development build
      [fhirbase](https://registry.hub.docker.com/u/fhirbase/fhirbase). Here
      there is no need to specify any tags. Just use the command
      below:

      ~~~bash
      sudo docker run --name=fhirbase -p 5433:5432 -d fhirbase/fhirbase
      ~~~

    * The third method is to build an image locally from
      [Dockerfile](https://github.com/fhirbase/fhirbase/blob/master/Dockerfile). First
      you have to clone FHIRbase project. Then go to the project
      folder, build an image with name 'fhirbase' and tag 'latest' and
      run docker.

      ~~~
      git clone https://github.com/fhirbase/fhirbase/
      cd fhirbase
      sudo docker build -t fhirbase:latest .
      sudo docker run --name=fhirbase -p 5433:5432 -d fhirbase/fhirbase
      ~~~

3.  Check installation

    The process of image loading can take some time. When it is
    finished FHIRbase will be accessible on localhost with the
    following parameters:

    - port: 5433
    - user: fhirbase
    - password: fhirbase

    You can check that your container is running, connect to FHIRbase
    and list database tables by the next commands:

    ~~~
    sudo docker inspect fhirbase
    # read <Config.NetworkSettings.IPAddress> and <Config.Image> of started container
    sudo docker run --rm -i -t <Config.Image> psql -h <Config.NetworkSettings.IPAddress> -U fhirbase -p 5432
    \dt
    ~~~

    or another way to connect to FHIRbase:

    ~~~bash
    psql -h localhost -p 5433 -U fhirbase
    \dt
    ~~~

    You will see tables of FHIR resources.
