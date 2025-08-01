FROM  debian:bullseye

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    wget build-essential git subversion \
    libjansson-dev uuid-dev libxml2-dev \
    libncurses5-dev libssl-dev \
    curl iputils-ping net-tools vim

# Install Asterisk
WORKDIR /usr/src
RUN git clone -b 18 https://github.com/asterisk/asterisk.git asterisk
WORKDIR /usr/src/asterisk
RUN contrib/scripts/get_mp3_source.sh && \
    contrib/scripts/install_prereq install && \
    ./configure && \
    make menuselect.makeopts && \
    menuselect/menuselect --enable CORE-SOUNDS-EN-ULAW \
                          --enable MOH-OPSOUND-ULAW \
                          --enable res_http_websocket \
                          menuselect.makeopts && \
    make -j$(nproc) && make install && make samples && make config

EXPOSE 5060/udp 5060/tcp 8088

CMD ["/usr/sbin/asterisk", "-f", "-vvv"]
