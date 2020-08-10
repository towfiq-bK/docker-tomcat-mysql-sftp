FROM ubuntu:14.04

RUN apt-get update
RUN apt-get install -y wget \
      && rm -rf /var/lib/apt/lists/*

# Prepare environment
ENV JAVA_HOME /usr/java/latest
ENV CATALINA_HOME /opt/tomcat
ENV CATALINA_BASE /opt/tomcat
ENV PATH $JAVA_HOME/bin:$CATALINA_HOME/bin:$CATALINA_HOME/scripts:$PATH

# ----------- JAVA INSTALLATION STARTED --------------
# JAVA VARIABLES
ENV JAVA_VERSION 11.0.7
ENV JAVA_BUILD 11.0.7+8
ENV JAVA_DL_HASH e51269e04165492b90fa15af5b4eb1a5

# Download JDK 11 and install from GooleDrive
RUN wget --load-cookies /tmp/cookies.txt \
          "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=1zXJqUd4E99WLuMVa5n8Gfo6B09fhWGV1' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=1zXJqUd4E99WLuMVa5n8Gfo6B09fhWGV1" \
          -O jdk-${JAVA_VERSION}_linux-x64_bin.tar.gz && rm -rf /tmp/cookies.txt
RUN tar xvzf jdk-${JAVA_VERSION}_linux-x64_bin.tar.gz && rm jdk-${JAVA_VERSION}_linux-x64_bin.tar.gz && mkdir -p /usr/java && mv jdk-${JAVA_VERSION} ${JAVA_HOME}

# ----------- TOMCAT INSTALLATION STARTED --------------
# TOMCAT VARIABLES
ENV TOMCAT_MAJOR 9
ENV TOMCAT_VERSION 9.0.29

# Download TOMCAT 8 and install
RUN wget --load-cookies /tmp/cookies.txt \
           "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=1n5v_jKljvoas99Z7F10vaR7PTdak2FYi' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=1n5v_jKljvoas99Z7F10vaR7PTdak2FYi" \
            -O apache-tomcat-${TOMCAT_VERSION}.tar.gz && rm -rf /tmp/cookies.txt
RUN tar -xvf apache-tomcat-${TOMCAT_VERSION}.tar.gz && rm apache-tomcat*.tar.gz && mv apache-tomcat* ${CATALINA_HOME}

RUN echo 'CATALINA_OPTS="-Xms512M -Xmx1024M -server -XX:+UseParallelGC -Dspring.profiles.active=dev"' > ${CATALINA_HOME}/bin/setenv.sh
RUN echo 'CATALINA_OPTS="-Xms256m -Xmx512m -XX:+UseParallelGC -Dspring.profiles.active=dev"' > ${CATALINA_HOME}/bin/setenv.bat
RUN chmod +x ${CATALINA_HOME}/bin/*sh

WORKDIR /opt/tomcat

# TOMCAT CONFIGURATIONS
COPY supporter/tomcat/tomcat-users.xml /opt/tomcat/conf/
COPY supporter/tomcat/context-manager.xml /opt/tomcat/webapps/manager/META-INF/context.xml
COPY supporter/tomcat/context-host-manager.xml /opt/tomcat/webapps/host-manager/META-INF/context.xml
COPY supporter/tomcat/web-manager.xml /opt/tomcat/webapps/manager/WEB-INF/web.xml
COPY supporter/tomcat/tomcat9.service /usr/lib/systemd/system/tomcat9.service

CMD ["catalina.sh", "start"]
RUN echo "Tomcat user: 'test-username' |  password: 'test-password'"
CMD ["catalina.sh", "run"]
