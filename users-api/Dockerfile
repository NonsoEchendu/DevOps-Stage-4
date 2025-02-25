# Stage 1: Build the Spring Boot application
FROM maven:3.8.6-openjdk-17 AS build-stage

# Set the working directory
WORKDIR /app

# Copy the Maven project files
COPY pom.xml .
COPY src ./src

# Build the application
RUN ./mvnw clean install

# Stage 2: Create a minimal runtime image
FROM openjdk:17-jdk-alpine

# Set the working directory
WORKDIR /app

# Copy the built JAR file from the build stage
COPY --from=build-stage /app/target/users-api-0.0.1-SNAPSHOT.jar .

# Copy the .env file from the parent directory
COPY ../.env .

# Expose the port specified in SERVER_PORT
EXPOSE 8083

# Set environment variables from .env file
ENV $(grep -v '^#' .env | xargs)

# Run the application
CMD ["sh", "-c", "java -jar users-api-0.0.1-SNAPSHOT.jar --server.port=${SERVER_PORT} --jwt.secret=${JWT_SECRET}"]