FROM krol/weblogic1036
# Maintainer
# ----------
MAINTAINER Carolina Guillen <guillen.carolina@gmail.com>

#ENV JVM /usr/java/jdk1.7.0_80
ENV INSTALL /u01/oracle/install
ENV OSB_ZIP ofm_osb_generic_11.1.1.7.0_disk1_1of1.zip
#ENV JAVA_HOME /usr/lib/jvm/java-7-oracle
ADD install/* $INSTALL/
ADD config/* $INSTALL/

WORKDIR $INSTALL

USER root
#RUN mkdir /u01/oracle/weblogic/osb
RUN chown -R oracle $INSTALL
USER oracle
RUN unzip $INSTALL/$OSB_ZIP
#RUN cp $INSTALL_OSB/oraInst.loc /etc/
# Disk1/ Disk2/


#RUN mkdir /u01/oracle/weblogic/oepe
RUN sh $INSTALL/Disk1/runInstaller -silent -responseFile $INSTALL/response_OSB.rsp -jreLoc /usr/java/jdk1.7.0_80
#RUN sh $INSTALL/Disk1/runInstaller -silent -responseFile $INSTALL/response_OSB.rsp -jreLoc /usr/java/jdk1.7.0_80

#RUN sh Disk1/runInstaller -silent -responseFile $INSTALL_OSB/response_OSB.rsp -jreLoc $JVM

#clean: Oracle Universal Installer from /tmp/OraInstall
#RUN rm -rf $INSTALL/*
