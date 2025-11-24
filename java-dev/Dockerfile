FROM rockylinux:9

RUN dnf install -y ncurses \
&& dnf install -y man-db


ARG JDK_URL="https://download.java.net/java/GA/jdk25.0.1/2fbf10d8c78e40bd87641c434705079d/8/GPL/openjdk-25.0.1_linux-x64_bin.tar.gz"
ARG JAVA_HOME=/opt/jdk

RUN curl -fsSL "$JDK_URL" -o jdk.tar.gz \
 && mkdir ${JAVA_HOME} \
 && tar xvf jdk.tar.gz -C ${JAVA_HOME} --strip-components=1 \
 && rm jdk.tar.gz

ENV JAVA_HOME=${JAVA_HOME}
ENV PATH=$PATH:"${JAVA_HOME}/bin"
# append source bash_profile to bashrc script or do something here

CMD [ "/bin/bash" ]
