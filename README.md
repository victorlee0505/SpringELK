## SpringBoot app with monitoring

## Setup
- Docker
- JDK8
- maven

## Stack (ELK)
- SpringBoot
- ElasticSearch
- Logstash
- Kibana
- prometheus (TODO)
- Jaeger    (TODO)

## How to run ?

1. Fire up Docker

2. Run project as is. REST endpoint should be up.
    - POST: localhost:8080/api/cal  
    `{"op": "P", "left": "3", "right": "4"}`
    - GET:  localhost:8080/api/mov

    - GET localhost:8080/fib/9
    this require a separate "microservice" to help solve fibonacci number
    https://github.com/victorlee0505/DummySpring.git (run this app as is.)
    to simulate call stack and tracable by jaeger

3. under project root
    $ cd docker
    $ docker-compose up

4. Done.

## What can i do?
This stack has multiple services

The services above are used by Kibana to visualize data.

## GUI
This is where Kibana is used

- acess Kibana GUI: http://localhost:5601/

    LOGS:    
    Click menu icon -> Kibana -> Discover
    it should say you have Elasticsearch data.
    enter "logstash" in the text box and click next to setup data source.
    choose timestamp on the next screen.
    
    Now, menu icon -> Kibana -> Discover, you should see the log shows up.

    Prometheus (TODO)

    Jaeger (TODO)

- access Jaeger: http://localhost:16686/
    This is where you can trace a distributed service (group of microservices)(GET localhost:8080/fib/9)