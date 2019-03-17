---
layout: post
title: "Docker Stack for Developer"
categories: [docker, orchestration]
tags: [docker, swarm]
---

### What is Docker Stack
{: style="text-align: justify"}
[What is the difference between docker stack and docker-compose](https://vsupalov.com/difference-docker-compose-and-docker-stack/)

### Step By Step

#### 1. Init Docker Swarm
    docker swarm init

#### 2. Create file docker-stack.yml
    version: '3'
        services:
        mongo:
            image: mongo:latest
        ports:
            - 27017:27017

        elasticsearch:
            image: elasticsearch:5-alpine
        ports:
            - 9200:9200
            - 9300:9300

#### 3. Deploy stack
    docker stack deploy -c docker-stack.yml dev_stack

#### 4. Check Service
    docker stack services dev_stack

#### 5. Check logs
    docker service logs -f dev_stack_mongo

#### 6. Test Connection
    nc -v localhost 27017
