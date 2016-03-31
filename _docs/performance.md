---
layout: default
title:  "Performance"
id: performance
order: 3
---

# FHIRBase Performance

Generally, FHIRBase performance mainly depends on PostgreSQL
configuration (TODO: explain configuration options). User should
expect that FHIRBase is a bit slower in CRUD operations than
general-purpose PostgreSQL setup because it stores additional
meta-data for each resource and also uses Stored Procedures instead of
vanilla SQL statements.

Resources stored in FHIRBase will consume a bit more disk space than
it's raw JSON representation - about 1.3 of it's original size. For
example, if you store 1 million of resources (1KB each), such table
will consume 1.3GB, not 1GB as you may expect. Additional indexes for
fast searches will consume additional space depending on type of
index.

Searching, one of most important operations, is optimized very well,
thanks to PostgreSQL GiN and GiST indices. It performs well on rather
complex searches with sorting and chained params.

Following table shows detailed timing which we get on m3.medium Amazon
EC2 Instance Type <https://aws.amazon.com/ec2/instance-types/#M3>.

| Operation                                                                                                           | Elapsed time (ms)      |
|---------------------------------------------------------------------------------------------------------------------+-----------------------:|{% for operation in site.data.performance.operations %}
| {{ operation.description }} | {{ operation.time }} |{% endfor %}
|---------------------------------------------------------------------------------------------------------------------|-------------------|
{: .table .table-condensed .table-benchmark .table-striped }

## Generating test data and running benchmarks on your machine

Fhirbase `perf` utility can be used on your machine
to generate test data:

~~~bash
path/to/fhirbase/perf/perf --verbose=3 \
                           --number-of-patients=1000000 \
                           --pgdatabase=your_db_name \
                           --pghost=locahost \
                           --pgpassword=your_password \
                           --pgport=5432 \
                           --pguser=your_user_name
~~~

This command will generate 1 million of Patients, 1.3 million of
Encounters, 200 Practitioners and 400 Organizations, and will
cross-link them with ResourceReferences. Usually it takes from 5 to
20 minutes to generate such amount of data.

Now you can run benchmark suite:

~~~bash
echo "SET plv8.start_proc = 'plv8_init'; SELECT SELECT fhir_benchmark('{}'::json);" \
     | psql postgres://your_user_name:your_password@localhost:5432/your_db_name
~~~

This operation can take some time, be patient.
