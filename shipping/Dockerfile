FROM maven:3.9.14 AS builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package &&  \
        mv target/shipping-1.0.jar shipping.jar

FROM eclipse-temurin:17.0.12_7-jre-alpine
EXPOSE 8080
WORKDIR /app
COPY --from=builder /app/shipping.jar .
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
# change the ownership of the application to the new user.
RUN chown -R roboshop:roboshop /app
USER roboshop
CMD ["java", "-jar", "shipping.jar"]
#ENVIROMENT WE ARE HANDLING IN THE K8S CONFIGMAP, SO WE ARE NOT DEFINING ENVIRONMENT VARIABLES IN THE DOCKERFILE.
