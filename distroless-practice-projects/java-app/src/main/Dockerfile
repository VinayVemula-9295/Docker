
# Stage 1: Build with Maven
FROM maven:3.9.3-eclipse-temurin-17 AS builder
WORKDIR /build
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2: Run with distroless
FROM gcr.io/distroless/java17
COPY --from=builder /build/target/*.jar app.jar
CMD ["app.jar"]
