# HEADER
FROM        linuxserver/wireshark
LABEL maintainer="wolfgang.tremmel@de-cix.net"

# Trigger rebuild
ENV         UPDATED_AT 2021-04-19

# Install netcat and net-tools
RUN		apk update \
		&& apk upgrade \
		&& apk add netcat-openbsd busybox-extras net-tools vim less
RUN		mkdir /etc/s6-overlay/s6-rc.d/inetdStart \
		&& echo "oneshot" > /etc/s6-overlay/s6-rc.d/inetdStart/type \
		&& echo "/usr/sbin/inetd" > /etc/s6-overlay/s6-rc.d/inetdStart/up \
		&& touch /etc/s6-overlay/s6-rc.d/user/contents.d/inetdStart

ADD  inetd-conf /etc/inetd.conf
# ADD  docker-entrypoint.sh /
