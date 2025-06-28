# Use Eclipse Temurin JDK 21 as base for building
FROM eclipse-temurin:21-jdk as builder

WORKDIR /app

# Copy project files into the image
COPY . .

# Make the Maven wrapper script executable
RUN chmod +x ./mvnw

# Build the application
RUN ./mvnw clean package -DskipTests

# Create a smaller runtime image
FROM eclipse-temurin:21-jre

WORKDIR /app

# Copy the built jar file from the builder image
COPY --from=builder /app/target/*.jar app.jar

# Expose port
EXPOSE 8080

# Run the app
ENTRYPOINT ["java", "-jar", "app.jar"]
