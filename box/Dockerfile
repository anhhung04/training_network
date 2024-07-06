FROM ubuntu:22.04
RUN apt-get update && apt-get install -y openssh-server  iptables net-tools dnsutils iproute2 iputils-ping python3 python3-pip tcpdump curl && apt-get clean 

RUN echo 'PasswordAuthentication yes' >> /etc/ssh/sshd_config
RUN echo 'PermitRootLogin yes' >> /etc/ssh/sshd_config

RUN echo -n "root:admin" | chpasswd

# Configure port forwarding
COPY entrypoint.sh /entrypoint.sh 
RUN chmod +x /entrypoint.sh
RUN update-alternatives --set iptables /usr/sbin/iptables-legacy
RUN sysctl -w net.ipv4.ip_forward=1
RUN sysctl -w net.ipv4.conf.all.route_localnet=1
EXPOSE 22

CMD ["/entrypoint.sh"]