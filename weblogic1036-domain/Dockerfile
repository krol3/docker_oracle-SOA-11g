FROM krol/weblogic1036

# Maintainer
# ----------
MAINTAINER Carolina Guillen <guillen.carolina@gmail.com>

# WLS Configuration
# -------------------------------
ENV ADMIN_PASSWORD welcome01
ENV ADMIN_PORT 7001
ENV NM_PORT 5556
ENV USER_MEM_ARGS -Xms256m -Xmx512m -XX:MaxPermSize=1024m
ENV EXTRA_JAVA_PROPERTIES $EXTRA_JAVA_PROPERTIES -Djava.security.egd=file:///dev/urandom
ENV JAVA_HOME /usr/java/jdk1.7.0_80/
# Add files required to build this image
COPY create-wls-domain.py /u01/oracle/

# Root commands
USER root
RUN echo ". $MW_1036/user_projects/domains/base_domain/bin/setDomainEnv.sh" >> /root/.bashrc && \
    echo "export PATH=$PATH:$MW_1036/wlserver_10.3/common/bin:$MW_1036/user_projects/domains/base_domain/bin" >> /root/.bashrc

# Configuration of WLS Domain
USER oracle
WORKDIR $MW_1036
RUN $MW_1036/wlserver_10.3/common/bin/wlst.sh -skipWLSModuleScanning /u01/oracle/create-wls-domain.py && \
    mkdir -p $MW_1036/user_projects/domains/base_domain/servers/AdminServer/security && \
    echo "username=weblogic" > $MW_1036/user_projects/domains/base_domain/servers/AdminServer/security/boot.properties && \
    echo "password=$ADMIN_PASSWORD" >> $MW_1036/user_projects/domains/base_domain/servers/AdminServer/security/boot.properties && \
    echo ". /u01/oracle/weblogic/user_projects/domains/base_domain/bin/setDomainEnv.sh" >> /u01/oracle/.bashrc && \
    echo "export PATH=$PATH:/u01/oracle/weblogic/wlserver_10.3/common/bin:/u01/oracle/weblogic/user_projects/domains/base_domain/bin" >> /u01/oracle/.bashrc

# Expose Node Manager default port, and also default http/https ports for admin console
EXPOSE $NM_PORT $ADMIN_PORT

# Final setup
WORKDIR /u01/oracle

ENV PATH $PATH:$MW_1036/user_projects/domains/base_domain/bin:/u01/oracle

# Define default command to start bash.
CMD ["startWebLogic.sh"]
