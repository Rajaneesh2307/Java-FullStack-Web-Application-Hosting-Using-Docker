FROM tomcat:9.0-jdk8-openjdk-slim

LABEL maintainer="Rajaneesh Yembuluru"
LABEL description="Hosting a java-fullstack-web-application"
LABEL version="1.0"

WORKDIR /usr/local/tomcat/webapps/
COPY vprofile-v2.war ROOT.war
EXPOSE 8080
CMD ["catalina.sh", "run"]
