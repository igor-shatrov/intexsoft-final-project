FROM ubuntu:18.04

# Make sure the package repository is up to date.
RUN apt-get update && \
    apt-get -qy full-upgrade && \
    apt-get install -qy git && \
# Install a basic SSH server
    apt-get install -qy openssh-server && \
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd && \
    mkdir -p /var/run/sshd && \
# Install JDK 8 
    apt-get install -qy openjdk-8-jdk && \
# Install maven
    apt-get install -qy maven && \
# Cleanup old packages
    apt-get -qy autoremove && \
# Add user jenkins to the image
    adduser --quiet jenkins && \
# Set password for the jenkins user 
    echo "jenkins:jenkins" | chpasswd
RUN apt-get install docker.io -y

#Add parametres for open privite git & docker repository without certificate
COPY .gitconfig /home/jenkins/.gitconfig
COPY daemon.json /etc/docker/daemon.json


# Standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
