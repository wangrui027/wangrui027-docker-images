##################### 镜像更新时需要修改的部分 #####################
FROM wangrui027/openjdk:8u442

ARG TOMCAT_VERSION=9.0.102

##################### 镜像更新时需要修改的部分 #####################

ARG TOMCAT_URL=https://mirrors.aliyun.com/apache/tomcat/tomcat-9/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz
ARG TOMCAT_HOME=/srv/tomcat
ARG TOMCAT_SERVER_XML=${TOMCAT_HOME}/conf/server.xml
ARG TOMCAT_CATALINA_SH=${TOMCAT_HOME}/bin/catalina.sh

ARG TGZ_PATH=/srv/apache-tomcat.tar.gz

RUN curl -o ${TGZ_PATH} --create-dirs ${TOMCAT_URL} && \
  tar -xvf ${TGZ_PATH} -C /srv && \
  rm ${TGZ_PATH} -rf && \
  ln -sf /srv/apache-tomcat-* ${TOMCAT_HOME} && \
  ln -sf ${TOMCAT_HOME}/webapps /srv/webapps && \
  sed -i 's/<Connector port="8080"/<Connector port="8080" URIEncoding="UTF-8"/g' ${TOMCAT_SERVER_XML} && \
  sed -i 's/#!\/bin\/sh/#!\/bin\/sh\n\nexport JAVA_OPTS="${JAVA_OPTS} \\\n\
    -Dfile.encoding=UTF8 -Dsun.jnu.encoding=UTF8 \\\n\
    -Djavax.sql.DataSource.Factory=org.apache.commons.dbcp.BasicDataSourceFactory \\\n\
    -Djava.util.prefs.userRoot=\/home\/tomcat\/preps \\\n\
    -Djava.security.egd=file:\/dev\/.\/urandom"\n/g' ${TOMCAT_CATALINA_SH} && \
  chmod +x ${TOMCAT_CATALINA_SH}

EXPOSE 8080

CMD ["/srv/tomcat/bin/catalina.sh", "run"]
