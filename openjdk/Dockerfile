ARG VERSION=latest
FROM ghcr.io/larryb02/rockylinux-base:${VERSION}

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

RUN dnf install -y maven

# TODO: find different approach for installing openjdk
# Java
ARG JAVA_HOME=/opt/jdk

RUN downloadUrl='https://download.java.net/java/GA/jdk25.0.1/2fbf10d8c78e40bd87641c434705079d/8/GPL/openjdk-25.0.1_linux-x64_bin.tar.gz'; \
    downloadSha256='2fbf10d8c78e40bd87641c434705079d'; \
    curl -fsSL "$downloadUrl" -o jdk.tar.gz; \
    mkdir ${JAVA_HOME}; \
    tar xvf jdk.tar.gz -C ${JAVA_HOME} --strip-components=1; \
    rm jdk.tar.gz;

ENV JAVA_HOME=${JAVA_HOME}
ENV PATH=${JAVA_HOME}/bin:$PATH
# smoke tests
RUN java --version; \
    javac --version