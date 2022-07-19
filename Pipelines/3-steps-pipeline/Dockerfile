#Download image from artifactory
ARG REGISTRY=http://artifactory-cluster.soleng-us.jfrog.team/artifactory
FROM openjdk:11-jdk
#FROM $REGISTRY/openjdk:11-jdk

WORKDIR /app

#Define ARG Again -ARG variables declared before the first FROM need to be declered again
ARG REGISTRY=http://artifactory-cluster.soleng-us.jfrog.team/artifactory
MAINTAINER Elad Hirsch

# Download artifacts from Artifactory
RUN curl $REGISTRY/libs-release-local/com/jfrog/backend/1.0.0/backend-1.0.0.jar --output server1.jar
RUN curl $REGISTRY/npm-dev-local/frontend/-/frontend-3.0.0.tgz --output client1.tgz

#Extract vue app
RUN tar -xzf client1.tgz && rm client1.tgz

# Set JAVA OPTS + Static file location
ENV STATIC_FILE_LOCATION="/app/package/target/dist/"
ENV JAVA_OPTS=""

# Fire up our Spring Boot app
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Dspring.profiles.active=remote -Djava.security.egd=file:/dev/./urandom -jar /app/server1.jar" ]
