FROM josedeng/ubuntu:ubuntu-15.10

ADD start.sh /start.sh

RUN dos2unix /start.sh && \
    chmod a+x /start.sh && \
    apt-get -q update && \
    apt-get -q -y install wget build-essential libpcre++-dev && \
    wget -q -O /tmp/installer.tar.gz \
         --no-check-certificate \
         --no-cookies \
         http://www.apache.org/dist/httpd/httpd-2.4.18.tar.gz && \
    wget -q -O /tmp/installer1.tar.gz \
         --no-check-certificate \
         --no-cookies \
         http://www.apache.org/dist/httpd/httpd-2.4.18-deps.tar.gz && \
    mkdir -p /opt/apache && \
    mkdir -p /tmp/apache && \
    tar -xzf /tmp/installer.tar.gz --strip-components=1 -C /tmp/apache/ && \
    tar -xzf /tmp/installer1.tar.gz --strip-components=2 -C /tmp/apache/srclib && \
    cd /tmp/apache/ && \
    /bin/bash -c "./configure --prefix=/opt/apache --with-included-apr" && \
    make && \
    make install && \
    chown -R developer:developer /opt/apache && \
    apt-get clean && \
    apt-get autoremove wget --purge -y && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/*

USER developer
EXPOSE 80

ENTRYPOINT ["/start.sh"]