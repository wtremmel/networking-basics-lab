# HEADER
FROM        ffeldhaus/wireshark
LABEL maintainer="wolfgang.tremmel@de-cix.net"

# Trigger rebuild
ENV         UPDATED_AT 2021-04-19

# Install netcat and net-tools
RUN         	apt-get update \
		&& apt-get install -y apt-utils \
		&& apt-get install -y netcat net-tools nvi less openbsd-inetd

ADD  inetd-conf /etc/inetd.conf
ADD  docker-entrypoint.sh /
