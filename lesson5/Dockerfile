FROM alpine:3 AS grandle
# Install Gradle

ENV GRADLE_VERSION 4.0

WORKDIR /gradle

RUN apk add -q --no-cache unzip=6.0-r4

RUN wget https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip
RUN unzip gradle-${GRADLE_VERSION}-bin.zip
RUN mv ./gradle-${GRADLE_VERSION} ./bin
RUN rm gradle-${GRADLE_VERSION}-bin.zip


# ------------------------------------------------------------------------------------
FROM alpine:3 AS allure
# Install Allure CLI

WORKDIR /allure

RUN apk add -q --no-cache unzip=6.0-r4

RUN wget https://github.com/allure-framework/allure-core/releases/download/allure-core-1.4.23/allure-commandline.zip
RUN unzip allure-commandline.zip
RUN rm allure-commandline.zip


# ------------------------------------------------------------------------------------
FROM java:8-jdk AS builder
# Prepare jars

ENV GRADLE_VERSION 4.0
ENV GRADLE_HOME /opt/gradle-${GRADLE_VERSION}
ENV MAIN_DIR /allure-docker-example

COPY --from=grandle /gradle/bin $GRADLE_HOME

WORKDIR /builder

WORKDIR ${MAIN_DIR}
COPY . .
RUN $GRADLE_HOME/bin/gradle


# ------------------------------------------------------------------------------------
FROM java:8-jdk
# Main image

LABEL Author="Dmytro Serdiuk"
LABEL Maintainer="dmytro.serdiuk@gmail.com"
LABEL Description="This image is used to show the Allure reposting"
LABEL Vendor="extsoft"
LABEL Version="1.1.0"

ENV MAIN_JAR 'allure-docker-example-1.1.0.jar'
ENV MAIN_DIR /allure-docker-example

COPY --from=allure /allure /
COPY --from=builder ${MAIN_DIR}/build/libs/${MAIN_JAR} ${MAIN_DIR}/build/libs/${MAIN_JAR}

WORKDIR /app

RUN groupadd -r docker && \
    useradd -r -g docker -d /app -s /sbin/nologin -c "Docker image user" docker && \
    chown -R docker:docker /app
USER docker

RUN cp ${MAIN_DIR}/build/libs/${MAIN_JAR} ./

RUN mkdir allure-report
RUN mkdir allure-result

RUN java -jar ${MAIN_JAR} || echo "Failed tests"
RUN allure generate -o allure-report allure-result

#Run tests, generate and open report
ENTRYPOINT allure report open -p 80
