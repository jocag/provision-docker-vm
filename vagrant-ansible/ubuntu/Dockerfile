FROM ubuntu:16.04
MAINTAINER "jocag@uma.es"
ENV container docker
ENV ANSIBLE_VERSION="2.2.2"
ENV PATH=/usr/bin/ansible:/etc/ansible:$PATH

RUN apt-get update && \
    apt-get install --no-install-recommends -y openssh-server openssh-client hostname initscripts sudo \
    gcc build-essential libssl-dev libffi-dev python python-dev python-yaml python-pip \
    rsyslog systemd systemd-cron lsb-release && \
    pip install -U pip setuptools && \
    pip install wheel virtualenv \
    ansible=="$ANSIBLE_VERSION" && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir /etc/ansible
RUN echo -e '[local]\nlocalhost ansible_connection=local' > /etc/ansible/hosts

# Add default vagrant user
RUN useradd --create-home -s /bin/bash vagrant
RUN echo -n 'vagrant:vagrant' | chpasswd
RUN echo 'vagrant ALL = NOPASSWD: ALL' > /etc/sudoers.d/vagrant
RUN chmod 440 /etc/sudoers.d/vagrant
RUN mkdir -p /home/vagrant/.ssh
RUN chmod 700 /home/vagrant/.ssh
RUN echo "ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA6NF8iallvQVp22WDkTkyrtvp9eWW6A8YVr+kz4TjGYe7gHzIw+niNltGEFHzD8+v1I2YJ6oXevct1YeS0o9HZyN1Q9qgCgzUFtdOKLv6IedplqoPkcmF0aYet2PkEDo3MlTBckFXPITAMzF8dJSIFo9D8HfdOV0IAdx4O7PtixWKn5y2hMNG0zQPyUecp4pzC6kivAIhyfHilFR61RGL+GPXQ2MWZWFYbAGjyiYJnAmCP3NOTd0jMZEnDkbUvxhMmBYSdETk1rRgm+R4LOzFUGaHqHDLKLX+FIPKcF96hrucXzcWyLbIbEgE98OHlnVYCzRdK8jlqm8tehUc9c9WhQ== vagrant insecure public key" > /home/vagrant/.ssh/authorized_keys
RUN chmod 600 /home/vagrant/.ssh/authorized_keys
RUN chown -R vagrant:vagrant /home/vagrant/.ssh
RUN sed -i -e 's/Defaults.*requiretty/#&/' /etc/sudoers
RUN sed -i -e 's/\(UsePAM \)yes/\1 no/' /etc/ssh/sshd_config
RUN echo 'LC_ALL=en_US.utf-8' >> /etc/default/locale
RUN systemctl enable ssh

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/sbin/init"]
