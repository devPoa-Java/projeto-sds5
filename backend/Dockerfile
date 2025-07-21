#FROM ubuntu:latest AS build
#RUN  apt-get update
#RUN  apt-get install openjdk-11-jdk -y
#COPY . .
#RUN  apt-get install maven -y
#RUN  mvn clean install
#FROM openjdk:11-jdk-slim 
#EXPOSE 8080
#COPY --from=build /target/dsvendas-0.0.1-SNAPSHOT.jar app.jar
#ENTRYPOINT [ "java", "-jar", "app.jar" ]

# Use the Eclipse temurin alpine official image
# https://hub.docker.com/_/eclipse-temurin
FROM eclipse-temurin:11-jdk-alpine

# Create and change to the app directory.
WORKDIR /app

# Copy local code to the container image.
COPY --from=build /target/dsvendas-0.0.1-SNAPSHOT.jar app.jar

# Build the app.
RUN ./mvnw -DoutputFile=target/mvn-dependency-list.log -B -DskipTests clean dependency:list install

# Run the app by dynamically finding the JAR file in the target directory
CMD ["sh", "-c", "java -jar target/*.jar"]

