FROM krol/weblogic1036

# Maintainer
# ----------
MAINTAINER Carolina Guillen <guillen.carolina@gmail.com>

ENV JVM /usr/java/jdk1.7.0_80
ENV INSTALL_OSB /u01/install
ENV OSB_ZIP ofm_osb_generic_11.1.1.7.0_disk1_1of1.zip

ADD install/* $INSTALL_OSB/
ADD config/* $INSTALL_OSB/

WORKDIR $INSTALL_OSB

USER root
RUN unzip $INSTALL_OSB/$OSB_ZIP
RUN chown -R oracle $INSTALL_OSB
RUN cp $INSTALL_OSB/oraInst.loc /etc/
# Disk1/ Disk2/

USER oracle
#RUN mkdir /u01/oracle/weblogic/oepe
RUN sh Disk1/runInstaller -silent -responseFile $INSTALL_OSB/response_OSB.rsp -jreLoc $JVM

RUN sh Disk1/runInstaller -silent -responseFile $INSTALL_OSB/response_OSB.rsp -jreLoc $JVM

#clean: Oracle Universal Installer from /tmp/OraInstall
RUN rm -rf $INSTALL_OSB/*
