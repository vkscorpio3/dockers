FROM josedeng/ubuntu:ubuntu-15.10

ADD start.sh /start.sh

ENV NODEJS_VERSION v4.4.3

RUN dos2unix /start.sh && \
    chmod a+x /start.sh && \
    apt-get -q update && \
    apt-get -q -y install wget xz-utils && \
    wget -q -O /tmp/installer.tar.xz \
         --no-check-certificate \
         --no-cookies \
         https://nodejs.org/dist/$NODEJS_VERSION/node-${NODEJS_VERSION}-linux-x64.tar.xz && \
    mkdir -p /opt/node-$NODEJS_VERSION && \
    tar -xJf /tmp/installer.tar.xz --strip-components=1 -C /opt/node-$NODEJS_VERSION && \
    chown -R developer:developer /opt/node-$NODEJS_VERSION && \
    /opt/node-$NODEJS_VERSION/bin/npm install -g gulp bower && \
    rm -rf ~/.npm/ && \
    apt-get clean && \
    apt-get autoremove wget xz-utils --purge -y && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/*

USER developer
VOLUME ["/opt/node-$NODEJS_VERSION"]

ENTRYPOINT ["/start.sh"]