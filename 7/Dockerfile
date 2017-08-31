FROM centos:latest
MAINTAINER yujmo yujmo94@gmail.com
RUN rm -rf /etc/yum.repos.d/CentOS-[DSfCMV]* \
    && yum clean all && yum update -y \
    && yum install openssh passwd openssl epel-release openssh-clients openssh-server -y \
    && yum clean all && yum update -y \
    && yum install nginx supervisor -y \
    && groupadd sftp && useradd -g sftp -s /bin/false web \
    && echo "admin" | passwd --stdin web \
    && mkdir -p /opt/sftp/web/ \
    && usermod -d /opt/sftp/web web \
    && chown root:sftp /opt/sftp/web \
    && chmod 755 /opt/sftp/web \
    && mkdir /opt/sftp/web/upload \
    && chown web:sftp /opt/sftp/web/upload \
    && chmod 755 /opt/sftp/web/upload \
    && rm -rf /etc/ssh/sshd_config /etc/nginx/conf.d/default.conf \
    && ssh-keygen -q -t rsa -b 2048 -f /etc/ssh/ssh_host_rsa_key -N '' \
    && ssh-keygen -q -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key -N '' \
    && ssh-keygen -t dsa -f /etc/ssh/ssh_host_ed25519_key -N '' 

COPY sshd_config /etc/ssh/sshd_config
COPY default.conf /etc/nginx/conf.d/default.conf
COPY index.html /opt/sftp/web/upload/index.html
COPY supervisord.conf /etc/supervisord.conf
EXPOSE 22 80 
CMD ["/usr/bin/supervisord"]
