FROM alpine:latest as builder

ARG version=3.1.0

ENV VERSION=$version

RUN apk add --no-cache \
    git \
    cmake \
    make \
    g++ \
    libressl-dev \
    lksctp-tools-dev \
    linux-headers

RUN cd /tmp && git clone https://github.com/aligungr/UERANSIM.git && \
    cd UERANSIM && git checkout tags/v$VERSION 

    
RUN cd /tmp/UERANSIM && echo "cmake --version" && make

FROM alpine:latest

COPY --from=builder /tmp/UERANSIM/build/* /usr/local/bin/

COPY /etc/ueransim /etc/ueransim
COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["/bin/sh"]
