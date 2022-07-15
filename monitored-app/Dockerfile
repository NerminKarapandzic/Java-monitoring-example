FROM openjdk:17-oracle

WORKDIR /app

#Copy mvn wrapper, we then don't need to have mvn installed on the machine
COPY .mvn/ .mvn
COPY mvnw pom.xml ./
COPY src ./src

#recording data will be saved here
RUN mkdir -p /recordings

RUN ./mvnw clean install -DskipTests

ENV BUILD_VERSION=0.0.1-SNAPSHOT
ENV BUILD_PATH=target/monitored-app
ENV JAR=$BUILD_PATH-$BUILD_VERSION.jar

ENTRYPOINT java -XX:StartFlightRecording:filename=/recordings/recordings.jfr,dumponexit=true -Dspring.profiles.active=${PROFILE} -jar ${JAR}

EXPOSE 8080