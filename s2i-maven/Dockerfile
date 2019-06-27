#FROM gins-dev/basebe:1.0
FROM openshift/base-centos7
#FROM java:8

ENV MAVEN_VERSION=3.6.0
ARG S2IDIR="/home/s2i"
ARG APPDIR="/deployments"

# Docker Image Metadata
LABEL io.k8s.description="Platform for building (Maven) and running plain Java applications" \
      io.k8s.display-name="Java Applications" \
      io.openshift.tags="builder,java,maven" \
      io.openshift.expose-services="8080" \
      org.jboss.deployments-dir="/deployments"

# Install Java
RUN INSTALL_PKGS="java-1.8.0-openjdk java-1.8.0-openjdk-devel" && \
    yum install -y $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y && \
    mkdir -p /opt/s2i/destination
	
#COPY ./settings.xml /usr/share/maven/conf

ADD ./target/*.jar app.jar

RUN chown -R 1001:1001 ./
#opt/app-root
USER 1001

EXPOSE 8090


# Run the jar file 
ENTRYPOINT ["java","-Dspring.profiles.active=dev -Doracle.jdbc.timezoneAsRegion=false","-jar","app.jar"]
