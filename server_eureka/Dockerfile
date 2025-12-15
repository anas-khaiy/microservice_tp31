# Étape 1 : Build avec Maven
FROM maven:3.8.4-eclipse-temurin-17 AS builder
WORKDIR /app

COPY pom.xml .
RUN mvn dependency:go-offline

COPY src ./src
RUN mvn clean package -DskipTests

# Étape 2 : Image finale
FROM eclipse-temurin:17-jdk-alpine
WORKDIR /app

COPY --from=builder /app/target/*.jar eureka-server.jar

ENTRYPOINT ["java", "-jar", "eureka-server.jar"]
