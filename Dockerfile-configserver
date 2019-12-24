FROM alpine-jdk:base 
MAINTAINER javaonfly 
COPY target/MicroserviceConfigServer-0.0.1-SNAPSHOT.jar /opt/lib/ 
RUN mkdir /var/lib/config-repo
COPY config-repo /var/lib/config-repo 
ENTRYPOINT ["/usr/bin/java"] 
CMD ["-jar", "/opt/lib/MicroserviceConfigServer-0.0.1-SNAPSHOT.jar.jar"] 
VOLUME /var/lib/config-repo 
EXPOSE 9090
