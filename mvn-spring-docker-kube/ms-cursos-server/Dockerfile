FROM openjdk:17-jdk-alpine as builder

WORKDIR /app/ms-cursos-server

COPY ./pom.xml /app

COPY ./ms-cursos-server/.mvn ./.mvn

COPY ./ms-cursos-server/mvnw .

COPY ./ms-cursos-server/pom.xml .

RUN ./mvnw clean package -Dmaven.test.skip  -Dmaven.main.skip -Dspring-boot.repackage.skip && rm -r ./target/

COPY ./ms-cursos-server/src ./src

RUN ./mvnw clean package -DskipTests

FROM openjdk:17-jdk-alpine

WORKDIR /app

RUN mkdir ./logs

COPY --from=builder /app/ms-cursos-server/target/ms-cursos-server-0.0.1-SNAPSHOT.jar .

EXPOSE 8002

CMD ["java", "-jar", "ms-cursos-server-0.0.1-SNAPSHOT.jar"]
