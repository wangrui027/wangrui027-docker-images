##################### 镜像更新时需要修改的部分 #####################
FROM wangrui027/almalinux:8

LABEL image.name=wangrui027/openjdk
LABEL image.tag=8u442

ADD OpenJDK8U-jdk_x64_linux_hotspot_8u442b06.tar.gz /usr/java

##################### 镜像更新时需要修改的部分 #####################

ENV JAVA_HOME /usr/java/latest
ENV CLASSPATH .:${JAVA_HOME}/lib/tools.jar:${JAVA_HOME}/jre/lib/dt.jar
ENV PATH ${JAVA_HOME}/bin:${PATH}

RUN ln -sf /usr/java/jdk* /usr/java/latest
