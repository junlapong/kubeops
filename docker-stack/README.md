# Docker Stack

[link to course](https://katacoda.com/kubeopsskills/courses/docker-workshop/docker-stack)

You've learned Basic Docker Stack by completing the following steps:

- Understanding Structure of Docker Compose
- Deploy Docker Stack
- Verifying and Cleanup Docker Stack

## Understanding Structure of Docker Compose

```yml
version: '3.8'

services:
    spring:
        image: sikiryl/spring-app
        ports:
            - 8081:8088

    kubeops-mysql:
        image: mysql:latest
        environment:
            - MYSQL_ROOT_PASSWORD=kubeops-root
            - MYSQL_USER=kubeops_user
            - MYSQL_PASSWORD=kubeops_password
            - MYSQL_DATABASE=kubeops
        volumes:
            - /tmp/mysql/data/:/var/lib/mysql
        ports:
            - 3307:3306
```

## Deploy Docker Stack

List all Docker Stacks on Kubernetes

```
docker stack ls
```

Deploy Docker Stack with deploy command

```
docker stack deploy kubeops-stack -c docker-compose.yaml
```

Waiting for around 1-2 minutes...

Get the status of each service in the stack

```
docker stack ps kubeops-stack
```

You'll see the status of each service in the stack is running.


## Verifying and Cleanup Docker Stack


Verifying if user is able to connect to the service in the stack

Waiting for around 8-10 minutes...

```
export IP=$(kubectl get services -l  com.docker.service.id=kubeops-stack-spring -o jsonpath='{ .items[*].status.loadBalancer.ingress[0].ip }')
curl http://$IP:8081
```

You'll got the message "Hello, KubeOps Skills"

Cleanup the stack with rm command

```
docker stack rm kubeops-stack
```
