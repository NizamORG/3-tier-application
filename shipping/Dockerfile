#
# Build
#
FROM maven:3.9.9-eclipse-temurin-8 AS build

WORKDIR /workspace

COPY pom.xml ./
RUN mvn -B -q -DskipTests dependency:go-offline

COPY src ./src
RUN mvn -B -q -DskipTests package

#
# Run
#
FROM eclipse-temurin:8-jre

EXPOSE 8080

WORKDIR /opt/shipping

ENV CART_ENDPOINT=cart:8080 \
    DB_HOST=mysql

COPY --from=build /workspace/target/shipping-1.0.jar /opt/shipping/shipping.jar

CMD [ "java", "-Xmn256m", "-Xmx768m", "-jar", "/opt/shipping/shipping.jar" ]

