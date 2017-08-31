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
    && tee /etc/ssh/sshd_config <<-'EOF'
    Protocol 2
    SyslogFacility AUTHPRIV
    PasswordAuthentication yes
    ChallengeResponseAuthentication no
    GSSAPIAuthentication yes
    GSSAPICleanupCredentials yes
    UsePAM yes
    AcceptEnv LANG LC_CTYPE LC_NUMERIC LC_TIME LC_COLLATE LC_MONETARY LC_MESSAGES
    AcceptEnv LC_PAPER LC_NAME LC_ADDRESS LC_TELEPHONE LC_MEASUREMENT
    AcceptEnv LC_IDENTIFICATION LC_ALL LANGUAGE
    AcceptEnv XMODIFIERS
    X11Forwarding yes
    Subsystem       sftp    internal-sftp
    Match Group sftp
    ChrootDirectory /opt/sftp/%u
    ForceCommand    internal-sftp
    AllowTcpForwarding no
    X11Forwarding no
    EOF
    
CMD ["/usr/sbin/sshd","-D"]
