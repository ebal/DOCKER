# The FROM instruction initializes a new build stage
FROM centos:6.9

# Install OpenSSH SSH daemon
RUN  yum clean all && ( yum check-update || true ) && yum -y install openssh-server

# Fixing sshd config file
RUN  sed -i -e 's/^UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config
RUN  sed -i -e 's/^#PermitRootLogin yes/PermitRootLogin yes/g' /etc/ssh/sshd_config

# Set root password
RUN  echo 'root:password' | chpasswd

# Create a host rsa public key
RUN  ssh-keygen -f /etc/ssh/ssh_host_rsa_key -N ''

# Export TCP Port 22
EXPOSE 22

# Run SSH Daemon to foreground
CMD ["/usr/sbin/sshd", "-D"]

