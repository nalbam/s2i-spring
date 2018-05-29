FROM openshift/base-centos7

MAINTAINER Jungyoul Yu <jungyouol.yu@bespinglobal.com>

EXPOSE 8080

ENV MAVEN_VERSION=3.5.3 \
    JAVA="java-1.8.0-openjdk java-1.8.0-openjdk-devel" \
    JAVA_TOOL_OPTIONS="-Dfile.encoding=UTF8" \
    APP_HOME=/apps \
    POM_PATH=.

LABEL io.k8s.description="Platform for building and running Spring Boot applications" \
      io.k8s.display-name="SpringBoot (openjdk 1.8)" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,java,springboot" \
      io.openshift.s2i.destination="/opt/s2i/destination"

# Install Maven, Java
RUN INSTALL_PKGS="tar unzip bc which lsof $JAVA" && \
    yum install -y --enablerepo=centosplus $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y && \
    (curl -v https://www.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | \
    tar -zx -C /usr/local) && \
    ln -sf /usr/local/apache-maven-$MAVEN_VERSION/bin/mvn /usr/local/bin/mvn && \
    mkdir -p $HOME/.m2 && \
    mkdir -p /app && \
    mkdir -p /opt/s2i/destination

# Add s2i maven customizations
ADD contrib $HOME/.m2/

# Copy the S2I scripts from the specific language image to $STI_SCRIPTS_PATH
COPY s2i $STI_SCRIPTS_PATH

RUN chown -R 1001:0 /app && chown -R 1001:0 $HOME && \
    chmod -R ug+rwx /app && \
    chmod -R g+rw /opt/s2i/destination

USER 1001

CMD $STI_SCRIPTS_PATH/usage
