FROM rockylinux:9 AS builder

RUN dnf install -y ncurses

FROM builder AS config

ARG JDK_VERSION=25.0.1
ARG JDK_ARCH=aarch64
ARG JDK_HASH=2fbf10d8c78e40bd87641c434705079d
ARG JDK_BUILD=8

ARG JDK_URL="https://download.java.net/java/GA/jdk${JDK_VERSION}/${JDK_HASH}/${JDK_BUILD}/GPL/openjdk-${JDK_VERSION}_linux-${JDK_ARCH}_bin.tar.gz"
ARG JAVA_HOME=/opt/jdk

RUN curl -fsSL "$JDK_URL" -o jdk.tar.gz \
 && mkdir ${JAVA_HOME} \
 && tar xvf jdk.tar.gz -C ${JAVA_HOME} --strip-components=1 \
 && rm jdk.tar.gz

ENV JAVA_HOME=${JAVA_HOME}
ENV PATH=$PATH:"${JAVA_HOME}/bin"


