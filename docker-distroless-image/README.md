# Docker Distroless Image

[link to course](https://katacoda.com/kubeopsskills/courses/docker-workshop)

`Dockerfile`

```docker
FROM gcr.io/distroless/java:11

COPY spring-distroless-app.jar deployment.jar
EXPOSE 8088

ENTRYPOINT ["java","-jar","./deployment.jar"]
```

```
docker build -t spring-distroless-app .
```

```
docker images | grep spring-distroless-app
```

```
docker run --name spring-distroless-app -d -p 8080:8088 junlapong/spring-distroless-app
```