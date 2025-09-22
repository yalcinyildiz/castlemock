#FROM tomcat:11.0.8-jdk21-temurin
FROM tomcat:11.0.5-jdk21-temurin-noble
LABEL MAINTAINER="Karl Dahlgren <karl.dahlgren@castlemock.com>"

ARG USER_NAME=tomcat
ARG GROUP_NAME=tomcat
ARG USER_ID=1001
ARG GROUP_ID=1001
ARG VERSION=1.68

# Create non-root user and group, and change the owner of tomcat folder
RUN groupadd -g ${GROUP_ID} ${GROUP_NAME} \
 && useradd -u ${USER_ID} -g ${GROUP_ID} -d /usr/local/tomcat -s /sbin/nologin ${USER_NAME} \
 && chown -R ${USER_NAME}:${GROUP_NAME} /usr/local/tomcat

# change workdir
WORKDIR /usr/local/tomcat

# Delete the default applications
RUN rm -rf /usr/local/tomcat/webapps/ROOT \
 && rm -rf /usr/local/tomcat/webapps/docs \
 && rm -rf /usr/local/tomcat/webapps/examples \
 && rm -rf /usr/local/tomcat/webapps/manager \
 && rm -rf /usr/local/tomcat/webapps/host-manager

# change workdir
WORKDIR /usr/local/tomcat/webapps
COPY --chown=${USER_NAME}:${GROUP_NAME} castlemock-v1.68.war castlemock.war

# Expose HTTP port 8080
EXPOSE 8080

# switch to non-root user
USER ${USER_NAME}:${GROUP_NAME}
