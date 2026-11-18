# ---- build ----
FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn -B -q dependency:go-offline
COPY src ./src
RUN mvn -B -q clean package -DskipTests

# ---- run ----
FROM eclipse-temurin:21-jre
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
# Keep memory low for free-tier hosts (512 MB)
ENV JAVA_TOOL_OPTIONS="-Xmx300m -XX:+UseSerialGC"
EXPOSE 8080
ENTRYPOINT ["java","-jar","app.jar"]
