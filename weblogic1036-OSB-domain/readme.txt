#build de image
docker build -t krol/weblogic1036-osb-domain .

#run the image
docker run --rm=true -it -p 7001:7001 krol/weblogic1036-domainadmin startWebLogic.sh

#teste the image
http://localhost:7001/console/login/LoginForm.jsp
user: oracle
passowrd: weblogic1

#material
https://docs.oracle.com/cd/E13222_01/wls/docs90/config_scripting/domains.html
https://ofmcanberra.wordpress.com/2014/06/12/creating-an-osb-domain-using-wlst/
https://github.com/Joelith/wlst/blob/master/OSB/osb_domain.py
http://www.qualogy.com/wlst-domain-creation-using-dry-run-2/
