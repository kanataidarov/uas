# uas

This is a User Authorization Service (UAS) - application intended to be part of a microservice architecture. 

Gateway Service - application intended to be part of a microservice architecture.

The application has following features: 
* It is based on JHipster UAA - a user accounting and authorizing service for securing microservices.
* It uses JSON Web Token ([JWT](https://jwt.io/introduction/)) authorization protocol.
* It is a fully configured authorization server with the users, roles, and corresponding endpoints inside. 
* The application is configured for Service Discovery and Configuration with the JHipster-Registry. On launch, it will refuse to start if it is not able to connect to the JHipster-Registry at [http://localhost:8761](http://localhost:8761). For more information on the JHipster Registry, read documentation on [https://www.jhipster.tech/jhipster-registry/](https://www.jhipster.tech/jhipster-registry/).

## Development

To start your application in the dev profile, run:

    ./gradlew

## Building for production

### Packaging as jar

To build the final jar and optimize the uas application for production, run:

    ./gradlew -Pprod clean bootJar

To ensure everything worked, run:

    java -jar build/libs/*.jar

### Packaging as war

To package your application as a war in order to deploy it to an application server, run:

    ./gradlew -Pprod -Pwar clean bootWar

## Testing

To launch your application's tests, run:

    ./gradlew test integrationTest jacocoTestReport

### Code quality

Cloud based [Sonar](https://sonarcloud.io/) is used to analyse code quality. 

You can start a local Sonar server (accessible on http://localhost:9001) with:

```
docker-compose -f src/main/docker/sonar.yml up -d
```
Also you can run a Sonar analysis with using the [sonar-scanner](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner) or by using the gradle plugin.

Then, run a Sonar analysis:

```
./gradlew -Pprod clean check jacocoTestReport sonarqube
```
## Using Docker for simple deployment (optional)

You can use Docker to improve your JHipster development experience. A number of docker-compose configuration are available in the [src/main/docker](src/main/docker) folder to launch required third party services.

For example, to start a postgresql database in a docker container, run:

    docker-compose -f src/main/docker/postgresql.yml up -d

To stop it and remove the container, run:

    docker-compose -f src/main/docker/postgresql.yml down

You can also fully dockerize your application and all the services that it depends on.
To achieve this, first build a docker image of your app by running:

    ./gradlew bootJar -Pprod jibDockerBuild

Then run:

    docker-compose -f src/main/docker/app.yml up -d

For more information refer to [Docker Documentation](https://docs.docker.com/). 

## Continuous Integration (optional)

The application structure fully supports CI pipeline for popular Continuous Integration systems (GitLab, GitHub, etc.).

GitLab CI configuration already included. For more information refer to [GitLab Documentation](https://docs.gitlab.com/).

