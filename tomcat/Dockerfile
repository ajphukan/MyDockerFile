FROM ubuntu

# ADD JAVA repo
RUN apt-get update && apt-get install -y curl \
software-properties-common \
&& add-apt-repository ppa:linuxuprising/java


# Install JAVA  
# and the below two line is to make the java installation silent without user intervention
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections \
&& echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections \
&& apt-get update && apt-get install -y oracle-java10-installer



# Install Tomcat

RUN mkdir -p /opt/tomcat \
&& curl -SL http://www-eu.apache.org/dist/tomcat/tomcat-9/v9.0.7/bin/apache-tomcat-9.0.7.tar.gz \
| tar -xzC /opt/tomcat --strip-components=1 \
&& rm -Rf /opt/tomcat/webapps/docs /opt/tomcat/webapps/examples


# COPY is used during the build process to move file from local to docker image
COPY tomcat-users.xml /opt/tomcat/conf/

# Expose tomcat  , It is a dockerfile keyword to expose port number
EXPOSE 8080

ENV JAVA_OPTS -server -XX:+DisableExplicitGC -XX:+UseConcMarkSweepGC \
-Xms1G -Xmx2G -XX:PermSize=1G -XX:MaxPermSize=2G

WORKDIR /opt/tomcat
CMD ["bin/catalina.sh", "run"]


# to build sudo docker build -t tomcat_serv:1.1 .
# to run sudo docker run -p 8080:8080 --name "Tomcat_Test" tomcat_serv:1.0
