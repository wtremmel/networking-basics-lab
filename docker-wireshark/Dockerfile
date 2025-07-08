# HEADER
FROM        linuxserver/wireshark
LABEL maintainer="wolfgang.tremmel@de-cix.net"

# Trigger rebuild
ENV         UPDATED_AT=2025-07-08

# Install netcat and net-tools
RUN		apk update \
		&& apk upgrade \
		&& apk add netcat-openbsd busybox-extras nmap-ncat net-tools vim less
RUN		mkdir /etc/s6-overlay/s6-rc.d/uechodStart \
		&& echo "longrun" > /etc/s6-overlay/s6-rc.d/uechodStart/type \
		&& echo "#!/command/execlineb -P" > /etc/s6-overlay/s6-rc.d/uechodStart/run \
		&& echo "/usr/bin/ncat -e /bin/cat -k -u -l 7" >> /etc/s6-overlay/s6-rc.d/uechodStart/run \
		&& touch /etc/s6-overlay/s6-rc.d/user/contents.d/uechodStart \
   		&& mkdir /etc/s6-overlay/s6-rc.d/techodStart \
		&& echo "longrun" > /etc/s6-overlay/s6-rc.d/techodStart/type \
		&& echo "#!/command/execlineb -P" > /etc/s6-overlay/s6-rc.d/techodStart/run \
		&& echo "/usr/bin/ncat -e /bin/cat -k -l 7" >> /etc/s6-overlay/s6-rc.d/techodStart/run \
		&& touch /etc/s6-overlay/s6-rc.d/user/contents.d/techodStart

ADD  inetd-conf /etc/inetd.conf
# ADD  docker-entrypoint.sh /
