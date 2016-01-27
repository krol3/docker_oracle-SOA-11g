#build the image
docker build -t krol/weblogic1036-osb .

#run the image
docker run --rm=true -it krol/weblogic1036-osb /bin/bash

#create a TAG OSB:1.0
docker tag ID krol/weblogic1036osb:1.0

#instalando manualmente : AFTER commit
docker  tag --force 1b71bb1298be krol/weblogic1036-osb

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
Preparing to launch Oracle Universal Installer from /tmp/OraInstall2016-01-27_09-17-33PM. Please wait ...Error in CreateOUIProcess(): 26
: Text file busy
[oracle@719686928ce5 install]$ sh Disk1/runInstaller -silent -responseFile /u01/install/response_OSB.rsp -jreLoc /usr/java/jdk1.7.0_80
Starting Oracle Universal Installer...

Checking if CPU speed is above 300 MHz.    Actual 2400 MHz    Passed
Checking Temp space: must be greater than 150 MB.   Actual 279940 MB    Passed
