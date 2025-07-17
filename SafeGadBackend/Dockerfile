# Stage 1: Build the application
FROM maven:3.9.9 AS build
WORKDIR /app
COPY CapStone_Semicolon/pom.xml .
# Download dependencies first, useful for caching
RUN mvn dependency:go-offline -B

# Copy the rest of the source code
COPY CapStone_Semicolon .
RUN mvn clean package -DskipTests

# Stage 2: Runtime stage
FROM openjdk:23
WORKDIR /app
# Copy the executable JAR from the build stage
COPY --from=build /app/target/*.jar SafeGadBackend.jar

# Set environment variables

ENV PORT=${PORT}

# Expose the port
EXPOSE ${PORT}

# Entry point to run the application
ENTRYPOINT ["java", "-jar", "-Dserver.port=${PORT}", "SafeGadBackend.jar"]