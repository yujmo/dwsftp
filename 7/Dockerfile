FROM centos:6
MAINTAINER yujmo yujmo94@gmail.com
RUN rm -rf /etc/yum.repos.d/CentOS-[DSfCMV]* \
    && yum clean all && yum update -y \
    && yum install openssh openssh-client openssh-server -y \
    && groupadd sftp && useradd -g sftp -s /bin/false web \
    && echo "admin" | passwd --stdin web \
    && mkdir -p /opt/sftp/web/ \
    && usermod -d /opt/sftp/web web \
    && chown root:sftp /opt/sftp/web \
    && chmod 755 /opt/sftp/web \
    && mkdir /opt/sftp/web/upload \
    && chown web:sftp /opt/sftp/web/upload \
    && chmod 755 /opt/sftp/web/upload \
    && rm -rf /etc/ssh/sshd_config    
ADD sshd_config /etc/ssh/sshd_config
CMD ["/usr/sbin/sshd","-D"]
