#build the image
docker build -t krol/weblogic1036-osb .

#run the image
docker run --rm=true -it krol/weblogic1036-osb /bin/bash

#create a TAG OSB:1.0
docker tag ID krol/weblogic1036osb:1.0

$
# installation without Reporting Feature or Oracle WS Manager Services
#DEV - environment using Derby

-silent

VOLUME /userDomain

sh runInstaller -silent -responseFile /u01/install/response_OSB.rsp -jreLoc /usr/java/jdk1.7.0_80

Disk1/runInstaller -silent -responseFile /u01/carol/test/response_OSB.rsp -jreLoc /usr/lib/jvm/java-7-oracle -invPtrLoc /home/carol/oracle/oraInventory/oraInst.loc

#links
https://cauhoi.wordpress.com/2012/03/13/how-to-install-oracle-service-bus-11-1-1-5-with-silent-option-on-linux-server/
http://myoracledbablogon.blogspot.com.br/2011/06/working-example-of-oracle-service-bus.html

---------problems ------------------
Preparing to launch Oracle Universal Installer from /tmp/OraInstall2015-10-22_12-44-46PM. Please wait ...Error in CreateOUIProcess(): 26
: Text file busy

/bin/cat: /proc/sys/net/core/wmem_default: No such file or directory
