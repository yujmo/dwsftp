FROM centos:6
RUN rm -rf /etc/yum.repos.d/CentOS-[DSfCMV]* \
    && yum clean all && yum update -y \
    && yum install openssh openssh-client openssh-server -y \
    && groupadd sftp && useradd -g sftp -s /bin/false web \
    && echo "admin" | passwd --stdin web \
    && mkdir -p /opt/sftp/web/ \
    && usermod -d /opt/sftp/web web
    && /etc/init.d/sshd restart
