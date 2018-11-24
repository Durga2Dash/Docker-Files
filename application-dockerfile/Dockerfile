FROM ubuntu:latest
MAINTAINER Murali Dhandapani <muralindia@gmail.com>

# Update and Install Java openjdk maven git lynx(optional)
RUN apt-get -y update && apt-get install -y curl wget openjdk-8-jdk  maven git lynx

# Create directory for Tomcat
RUN mkdir /usr/local/tomcat

# Download tomcat
RUN wget http://mirrors.estointernet.in/apache/tomcat/tomcat-8/v8.0.53/bin/apache-tomcat-8.0.53.tar.gz -O /tmp/tomcat.tar.gz

# Untar the downloaded Tomcat file
RUN cd /tmp && tar xvfz tomcat.tar.gz

# Copy the tomcat files to the directory created earlier
RUN cp -Rv /tmp/apache-tomcat-8.0.53/* /usr/local/tomcat/

# Expose port 8080 of the container
EXPOSE 8080

# Cloning Java application from github
RUN git clone https://github.com/muralindia/registration-login-java-xml-maven-jsp-mysql.git /tmp/project

# Working directory for packaging Java application
WORKDIR /tmp/project

# Building Java application using maven
RUN mvn package

# Copying war file to tomcat webapps directory
RUN cp /tmp/project/target/account-1.0-SNAPSHOT.war /usr/local/tomcat/webapps/application.war

# Starting tomcat
CMD /usr/local/tomcat/bin/catalina.sh run
