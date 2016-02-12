FROM oraclelinux:7

# Maintainer
MAINTAINER Carolina Guillen <guillen.carolina@gmail.com>

# Environment variable
ENV JAVA_RPM jdk-7u80-linux-x64.rpm
ENV WLS_JAR wls1036_generic.jar
ENV INSTALL /u01/install
ENV CONFIG_JVM_ARGS -Djava.security.egd=file:/dev/./urandom
ENV MW_1036 /u01/oracle/middleware1036

#root
RUN echo "root:root" | chpasswd
USER root

#basic packages
RUN yum install -y unzip

# SETUP FILESYSTEM AND ORACLE USER
RUN mkdir /u01 && chmod a+xr /u01 && \
    useradd -b /u01 -m -s /bin/bash oracle

# Copy packages
ADD config/* $INSTALL/
ADD install/* $INSTALL/

# Install and configure Oracle JDK
RUN rpm -i $INSTALL/$JAVA_RPM

# Adjust file permissions, go to /u01 as user 'oracle' to proceed with WLS installation
RUN chown oracle:oracle -R /u01

# Installation of Weblogic
USER oracle
RUN java -jar $INSTALL/$WLS_JAR -mode=silent -silent_xml=$INSTALL/silent.xml

WORKDIR /u01/oracle/middleware1036
RUN rm -r $INSTALL/

ENV PATH $PATH:$MW_1036/oracle_common/common/bin

# Define default command to start bash.
CMD ["bash"]
