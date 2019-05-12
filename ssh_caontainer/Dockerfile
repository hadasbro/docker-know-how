# ssh container
FROM ubuntu
MAINTAINER Slawek

RUN apt-get update && \
	apt-get install -y openssh-server openssl vim nano && \
	apt-get clean && \
	useradd -m -s /bin/bash -p $(openssl passwd -1 connection) sshclient
RUN mkdir /var/run/sshd

EXPOSE 22

CMD bash -c "/usr/sbin/sshd -D"
