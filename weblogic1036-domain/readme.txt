#build de image
docker build -t krol/weblogic1036-domain .

#run the image
docker run --rm=true -it -p 7001:7001 krol/weblogic1036-domain startWebLogic.sh

#teste the image
http://localhost:7001/console/login/LoginForm.jsp

--------- weblogic domain -------------
DOMAIN TEMPLATE: /u01/oracle/weblogic/wlserver_10.3/common/templates/domains/wls.jar
DOMAIN PATH: /u01/oracle/weblogic/user_projects/domains/base_domain
ADMIN PORT: 7001
ADMIN USER: weblogic
ADMIN PASSWORD: welcome01

http://localhost:7001/console

Development Mode
Sun SDK 1.6.0_45 @ /usr/java/jdk1.6.0_45

---------------------------------
java -jar wls1036_generic.jar -mode=silent -silent_xml=/home/carol/repository/bitbucket-krol/ws-docker/middleware11g/weblogic/config/silent_local.xml
