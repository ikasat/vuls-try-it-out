FROM centos:7

RUN set -x && \
    useradd -m vuls

RUN set -x && \
    yum install -y openssh-server && \
    /usr/sbin/sshd-keygen

# for deep scan
RUN set -x && \
    yum install -y sudo which yum-plugin-changelog yum-plugin-ps

COPY sudoers-vuls /etc/sudoers.d/sudoers-vuls

RUN set -x && \
    chmod 440 /etc/sudoers.d/sudoers-vuls
