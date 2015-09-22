FROM tomcat:8.0

ENV MAVEN_VERSION 3.3.3

RUN curl -fsSL http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar xzf - -C /usr/share \
  && mv /usr/share/apache-maven-$MAVEN_VERSION /usr/share/maven \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_HOME /usr/share/maven
ENV JAVA_OPTS -Xmx512m -Djava.security.egd=file:/dev/./urandom

RUN  mkdir -p /usr/local/tomcat/conf/Catalina/localhost
COPY ./src/main/docker/petclinic.xml  /usr/local/tomcat/conf/Catalina/localhost/petclinic.xml

COPY . /tmp/

RUN cd /tmp && /usr/bin/mvn package

COPY target/PetClinic.war /usr/local/tomcat/webapps/petclinic.war

CMD ["catalina.sh", "run"]
