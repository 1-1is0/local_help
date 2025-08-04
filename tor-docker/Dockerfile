FROM alpine:latest


RUN echo 'https://mirror.yandex.ru/mirrors/alpine/latest-stable/main'     > /etc/apk/repositories && \
    echo 'https://mirror.yandex.ru/mirrors/alpine/latest-stable/community'     >> /etc/apk/repositories && \
    echo '@edge https://mirror.yandex.ru/mirrors/alpine/edge/community' >> /etc/apk/repositories && \
    echo '@edge https://mirror.yandex.ru/mirrors/alpine/edge/testing'   >> /etc/apk/repositories
RUN apk -U upgrade
RUN apk -v add tor@edge obfs4proxy@edge curl
RUN apk -v add nmap
RUN apk add busybox-extras
RUN chmod 700 /var/lib/tor && \
    rm -rf /var/cache/apk/*
RUN tor --version

COPY --chown=tor:root torrc /etc/tor/

HEALTHCHECK --timeout=10s --start-period=60s \
    CMD curl --fail --socks5-hostname localhost:9050 -I -L 'https://www.facebookwkhpilnemxj7asaniu7vnjjbiltxjqhye3mhbshg7kx5tfyd.onion/' || exit 1

USER tor
EXPOSE 9053/udp 9050/tcp

CMD ["/usr/bin/tor", "-f", "/etc/tor/torrc"]

