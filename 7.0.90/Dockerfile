FROM inutano/wget:latest AS downloader

RUN wget -q https://archive.apache.org/dist/tomcat/tomcat-7/v7.0.90/bin/apache-tomcat-7.0.90.tar.gz --no-check-certificate
RUN tar xf apache-tomcat-7.0.90.tar.gz

#final build
FROM pristtlt/java:1.8

COPY --from=downloader /apache-tomcat-7.0.90 /usr/local/apache-tomcat-7.0.90

ENV CATALINA_HOME /usr/local/apache-tomcat-7.0.90/
ENV PATH $CATALINA_HOME/bin:$PATH
RUN rm -rf ${CATALINA_HOME}/webapps/*
WORKDIR ${CATALINA_HOME}/webapps

# let "Tomcat Native" live somewhere isolated
ENV TOMCAT_NATIVE_LIBDIR $CATALINA_HOME/native-jni-lib
ENV LD_LIBRARY_PATH ${LD_LIBRARY_PATH:+$LD_LIBRARY_PATH:}$TOMCAT_NATIVE_LIBDIR

EXPOSE 8080
CMD ["catalina.sh", "run"]
