# Stage 1: Build with Maven
FROM maven:3.9.6-eclipse-temurin-17 AS builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2: Create the final image
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
VOLUME /tmp

# Copy the JAR from the builder stage
COPY --from=builder /app/target/*.jar app.jar

# Expose port
EXPOSE 8085

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
