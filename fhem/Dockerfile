FROM debian:jessie

MAINTAINER Christian Görke 

ENV FHEM_VERSION 5.8
ENV DEBIAN_FRONTEND noninteractive

# Install dependencies
RUN apt-get update && apt-get upgrade -y --force-yes && apt-get install -y --force-yes --no-install-recommends apt-utils
RUN apt-get -y --force-yes install \
perl \
wget \
git \
apt-transport-https \
sudo etherwake \
dfu-programmer \
build-essential \
snmpd \
snmp \
vim \
telnet \
usbutils \
sqlite3

# Install perl packages
RUN apt-get -y --force-yes install \
libavahi-compat-libdnssd-dev \
libalgorithm-merge-perl \
libclass-dbi-mysql-perl \
libclass-isa-perl \
libcommon-sense-perl \
libdatetime-format-strptime-perl \
libdbi-perl \
libdevice-serialport-perl \
libdpkg-perl \
liberror-perl \
libfile-copy-recursive-perl \
libfile-fcntllock-perl \
libio-socket-ip-perl \
libio-socket-ssl-perl \
libjson-perl \
libjson-xs-perl \
libmail-sendmail-perl \
libsocket-perl \
libswitch-perl \
libsys-hostname-long-perl \
libterm-readkey-perl \
libterm-readline-perl-perl \
libwww-perl \
libxml-simple-perl \
libdbd-sqlite3-perl \
libtext-diff-perl

# Install fhem
RUN echo Europe/Berlin > /etc/timezone && dpkg-reconfigure tzdata

RUN wget https://fhem.de/fhem-${FHEM_VERSION}.deb && dpkg -i fhem-${FHEM_VERSION}.deb
RUN userdel fhem

VOLUME ["/opt/fhem"]

WORKDIR "/opt/fhem"

COPY start.sh /opt/fhem/start.sh
COPY ./data/contrib/dblog/db.conf /opt/fhem/contrib/dblog/db.conf

EXPOSE 8083

CMD bash /opt/fhem/start.sh
