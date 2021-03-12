## SpringBoot app with monitoring

## Setup
- Docker
- JDK8
- maven

## Stack (ELK)
- SpringBoot
- ElasticSearch
- APM Server
- Logstash
- Kibana
- prometheus 
- Jaeger    

## How to run ?

#### 1. Fire up Docker Desktop (if not already)

#### 2. Run project as is. REST endpoint should be up.
- POST: localhost:8080/api/cal

    `{"op": "+", "left": "3", "right": "4"}`
- GET:  localhost:8080/api/mov

- GET localhost:8080/fib/9
    this require a separate "microservice" to help solve fibonacci number
    https://github.com/victorlee0505/DummySpring.git (run this app as is.)
    to simulate call stack and tracable by jaeger

#### 3. under project root
```cmd
    $ cd docker
    $ docker-compose up
```

#### 4. Not Done. ELK security is enabled, so we need to setup password.
* go to Docker Desktop
* under the stack of app from our docker-compose
* point to elasticsearch , click the 2nd icon (CLI)
* you are now inside elasticsearch
* run this
```bash
      bin/elasticsearch-setup-passwords auto
```
* this will auto generate all password in the stack but you only care 1 of them
* user "elastic" , note down the password
* #### change all "changeme" occurrence inside docker folder
* restart docker-compose
5. Now the whole stack should be in working order. Done.


## What can i do?
This stack has multiple services

The services above are used by Kibana to visualize data.

## GUI
This is where Kibana is used

- acess Kibana GUI: http://localhost:5601/

login with user:elastic password: the one you generated

1. execute some REST on our app.
2. click menu button, go to the bottom, click **"Stack Management"**
    - click **"Index Management"** you should see something like.._logstash, apm, metricbeat_..
    - this is great, we already have some data.
    - click **"Index Patterns"** , this is where we make data searchable
    - click **Create index pattern**, type logstash*, choose type @timestamp and create.

3. now let's have some fun.
 click on menu button
* Analytic -> Discover; pick **logstash***, you can search the index pattern you just created
* Analytic -> Dashboard; search **prometheus** and choose the result returned, play with it.
* Observability -> Metrics : some metrics
* Observability -> APM : jaeger tracing

This is it.
