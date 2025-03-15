# 基础镜像声明（兼容CentOS 8）
FROM almalinux:8

# 元数据标签
LABEL maintainer="wangrui027@outlook.com"
LABEL description="AlmaLinux 8 with AliYun mirror and essential tools"

# 配置阿里云镜像源（核心优化）
RUN sed -e 's|^mirrorlist=|#mirrorlist=|g' \
  -e 's|^# baseurl=https://repo.almalinux.org|baseurl=https://mirrors.aliyun.com|g' \
  -i.bak \
  /etc/yum.repos.d/almalinux*.repo

# 设置时区（北京）
ENV TZ=Asia/Shanghai
RUN dnf install -y tzdata && \
  ln -sf /usr/share/zoneinfo/$TZ /etc/localtime && \
  echo $TZ > /etc/timezone

# 批量安装工具包（合并操作减少镜像层）
RUN dnf install epel-release -y && \
  dnf config-manager --set-enabled powertools && \
  dnf install \
  zip \
  unzip \
  wget \
  iputils \
  telnet \
  net-tools \
  findutils \
  fontconfig \
  gdal -y && \
  dnf clean all && \
  rm -rf /var/cache/dnf

RUN echo "alias ls='ls --color=auto'" >> /root/.bashrc && \
  echo "alias ll='ls -l --color=auto'" >> /root/.bashrc && \
  echo "alias la='ls -A --color=auto'" >> /root/.bashrc
