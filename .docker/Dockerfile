FROM tomcat:9.0.37-jdk11-corretto

RUN echo 'CATALINA_OPTS="-Xms512M -Xmx1024M -server -XX:+UseParallelGC -Dspring.profiles.active=dev"' > ${CATALINA_HOME}/bin/setenv.sh
RUN echo 'CATALINA_OPTS="-Xms256m -Xmx512m -XX:+UseParallelGC -Dspring.profiles.active=dev"' > ${CATALINA_HOME}/bin/setenv.bat
CMD ["catalina.sh", "start"]
CMD ["catalina.sh", "run"]
