FROM ylinux6.5.0-base:latest
MAINTAINER Maestrano <it@maestrano.com>

ENV PATH /bin/bash:$PATH
# Install Ansible
RUN wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm && \
    sudo rpm -iv epel-release-latest-6.noarch.rpm && \
    mkdir -p /etc/ansible/ &&  \
    yum -y install ansible && \
    yum -y install kernel-devel.x86_64 && \
    yinst start ylock_kern

# Add ansible configuration

ADD  playbooks/docker_container   /etc/ansible/playbooks/docker_container

WORKDIR /etc/ansible

RUN ansible-playbook /etc/ansible/playbooks/docker_container/site.yml -c local

# Expose port 22 and 80
EXPOSE 22 80


RUN  chmod 755 /etc/ansible/playbooks/docker_container/roles/test/files/init.sh

ENTRYPOINT ["/etc/ansible/playbooks/docker_container/roles/test/files/init.sh"]

