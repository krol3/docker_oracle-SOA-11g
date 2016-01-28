FROM oraclelinux:7

# Maintainer
# ----------
MAINTAINER Carolina Guillen <guillen.carolina@gmail.com>

# Environment variables required for this build (do NOT change)
# -------------------------------------------------------------
ENV JAVA_RPM jdk-7u80-linux-x64.rpm
ENV WLS_JAR wls1036_generic.jar
ENV JAVA_HOME /usr/java/default
ENV MW_HOME /u01/oracle/wls1036
ENV CONFIG_JVM_ARGS -Djava.security.egd=file:/dev/./urandom
ENV MW_1036 /u01/oracle/middleware1036

#root
# Pre-requirements
RUN echo "root:root" | chpasswd
USER root

RUN yum install -y unzip

# SETUP FILESYSTEM AND ORACLE USER
# ------------------------------------------------------------
RUN mkdir /u01 && chmod a+xr /u01 && \
    useradd -b /u01 -m -s /bin/bash oracle \
    mkdir /u01/oracle/wls1036

# Copy packages
ADD config/silent.xml $MW_HOME/
ADD install/$WLS_JAR $MW_HOME/
ADD install/$JAVA_RPM /u01/

# Install and configure Oracle JDK 8u25
# -------------------------------------
RUN rpm -i /u01/$JAVA_RPM && \
    rm /u01/$JAVA_RPM

# Adjust file permissions, go to /u01 as user 'oracle' to proceed with WLS installation
RUN chown oracle:oracle -R /u01

# Installation of Weblogic
USER oracle
WORKDIR /u01/oracle/
RUN java -jar $MW_HOME/$WLS_JAR -mode=silent -silent_xml=$MW_HOME/silent.xml
RUN ln -s $MW_1036 /u01/oracle/weblogic

WORKDIR /u01/oracle/weblogic
RUN rm $MW_HOME/$WLS_JAR

WORKDIR /u01/oracle

ENV PATH $PATH:/u01/oracle/weblogic/oracle_common/common/bin

# Define default command to start bash.
CMD ["bash"]
