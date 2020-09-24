FROM gcr.io/distroless/java:11

COPY spring-distroless-app.jar deployment.jar
EXPOSE 8088

ENTRYPOINT ["java","-jar","./deployment.jar"]
