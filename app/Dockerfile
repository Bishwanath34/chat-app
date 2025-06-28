# Use Eclipse Temurin JDK 21 (official base image for Java 21)
FROM eclipse-temurin:21-jdk as builder

# Set working directory
WORKDIR /app

# Copy everything to the container
COPY . .

# Package the Spring Boot app using Maven (skip tests for faster build)
RUN ./mvnw clean package -DskipTests

# Create a new minimal image from JDK runtime
FROM eclipse-temurin:21-jre

# Set working directory in runtime container
WORKDIR /app

# Copy the jar from the builder image
COPY --from=builder /app/target/*.jar app.jar

# Expose port
EXPOSE 8080

# Run the app
ENTRYPOINT ["java", "-jar", "app.jar"]
