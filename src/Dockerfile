FROM tomcat:9-jre8-alpine

RUN apk --update add curl ca-certificates tar 
RUN set -x \
    && mkdir /home/mysql \
    && curl -fSL https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.40.tar.gz -o /home/mysql/mysql-connector.jar \
    && cd /home/mysql \
    && tar -xzvf mysql-connector.jar \
    && pwd \
    && mkdir -p /usr/share/java \
    && mv /home/mysql/mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar /usr/share/java/mysql-connector-java.jar \
    && cd /home \
    && rm -R *

RUN export CLASSPATH=$CLASSPATH:/usr/share/java/mysql-connector-java.jar

# DEFAULT VALUES MUST BE OVERRIDEN FROM DOCKER RUN
ENV CONN_STRING "jdbc:mysql://mydb0123.mysql.database.azure.com:3306/alm"
ENV CONN_USER "user@mydb0123"
ENV CONN_PASSWORD "password"

RUN rm -R /usr/local/tomcat/webapps/*

ADD ./target/myshuttledev.war /usr/local/tomcat/webapps/ROOT.war

