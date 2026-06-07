# Option: openjdk:21-slim + Multi-stage + Spring Boot
FROM eclipse-temurin:21-jdk-alpine AS builder
WORKDIR /app
COPY pom.xml ./
RUN mvn dependency:go-offline -q
COPY . .
RUN mvn package -DskipTests

FROM eclipse-temurin:21-jre-alpine AS runtime
RUN addgroup -S sre_group && adduser -S sre_user -G sre_group
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar
USER sre_user
EXPOSE 8080
ENTRYPOINT ["java","-jar","app.jar"]