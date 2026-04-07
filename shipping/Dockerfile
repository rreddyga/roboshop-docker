# FROM maven:3.9.14
# Expose 8080
# WORKDIR /app
# COPY pom.xml .
# COPY src ./src
# RUN mvn clean package
# RUN mv target/shipping-1.0.jar shipping.jar
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
# CMD ["java", "-jar", "shipping.jar"]

# Stage 1: Build (Maven)
FROM maven:3.9.14-eclipse-temurin-21-alpine AS builder
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline -B
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2: Run (Minimalistic JRE only)
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=builder /app/target/shipping-1.0.jar shipping.jar

ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"

EXPOSE 8080
CMD ["java", "-jar", "shipping.jar"]