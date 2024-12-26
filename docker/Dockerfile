# Stage 1: Build the application
FROM maven:3.9.9-eclipse-temurin-21 AS build

# Set the working directory to /app
WORKDIR /app

# Copy the pom.xml file and install dependencies
COPY backend/pom.xml /app/pom.xml
RUN mvn dependency:go-offline -B

# Copy the backend directory contents into the container at /app
COPY backend /app

# Package the application
RUN mvn clean package -DskipTests -B

# Stage 2: Run the application
FROM eclipse-temurin:21-jre-alpine

# Set the working directory to /app
WORKDIR /app

# Copy the JAR file from the build stage
COPY --from=build /app/target/selenium_ejer1-0.0.1-SNAPSHOT.jar /app/selenium_ejer1-0.0.1-SNAPSHOT.jar

# Expose port 8080
EXPOSE 8080

# Run the Spring Boot application
ENTRYPOINT ["java", "-jar", "selenium_ejer1-0.0.1-SNAPSHOT.jar"]