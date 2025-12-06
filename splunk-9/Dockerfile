# Requirements: Debian 13.3 Trixie : podman pull debian
# Download splunk enterprise 9.4.x DEB package to the install/ directory

FROM debian
MAINTAINER J "oozer@mud.pile"

ENV DEBIAN_FRONTEND=noninteractive

# Use the newest packages
RUN apt-get update
RUN apt-get install -y wget gnupg locales curl sudo libgssapi-krb5-2 busybox procps acl gcc make \
  libffi-dev libssl-dev make build-essential libbz2-dev \
  xz-utils ca-certificates zlib1g-dev python3-apt p11-kit liblz4-dev \
  libhogweed6t64 libgnutls30t64 libgcrypt-bin python3-apt python3-pip

RUN echo "en_US.UTF-8 UTF-8" >/etc/locale.gen
RUN localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

# Setup the volume, make sure a splunk DEB package exists in .
RUN mkdir -p /opt/install /opt/splunk
ADD install /opt/install

# Install splunk enterprise, volume /opt/splunk should already exist, containing the package in install/
RUN dpkg -i /opt/install/splunk-*.deb
VOLUME ["/opt/splunk"]

# Edit install/user-seed.conf with a different plaintext password
RUN chown -R splunk:splunk /opt/splunk
COPY install/user-seed.conf /opt/splunk/etc/system/local
COPY install/search/local /opt/splunk/etc/apps/search/local

EXPOSE 8000
CMD /opt/splunk/bin/splunk --accept-license start && tail -f /opt/splunk/var/log/splunk/splunkd.log

