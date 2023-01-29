# FROM counterparty/base

FROM ubuntu:22.04
# FROM ubuntu:16.04

# MAINTAINER Counterparty Developers <dev@counterparty.io>

# Install common dependencies
RUN apt-get update && apt-get install -y apt-utils ca-certificates wget curl git mercurial \
    python3 python3-dev python3-pip python3-setuptools python3-appdirs \
    build-essential vim unzip software-properties-common sudo gettext-base \
    net-tools iputils-ping telnet lynx locales

# Upgrade pip3 to newest
RUN pip3 install --upgrade pip

# Set locale
RUN dpkg-reconfigure -f noninteractive locales && \
    locale-gen en_US.UTF-8 && \
    /usr/sbin/update-locale LANG=en_US.UTF-8
ENV LC_ALL en_US.UTF-8

# Set home dir env variable
ENV HOME /root


# install bitcoin core

# ENV BITCOIN_VER="0.21.1"
# ENV BITCOIN_FOLDER_VER="0.21.1"
# ENV BITCOIN_SHASUM="366eb44a7a0aa5bd342deea215ec19a184a11f2ca22220304ebb20b9c8917e2b"

ENV BITCOIN_VER="0.21.0"
ENV BITCOIN_FOLDER_VER="0.21.0"
ENV BITCOIN_SHASUM="da7766775e3f9c98d7a9145429f2be8297c2672fe5b118fd3dc2411fb48e0032"


WORKDIR /tmp

RUN wget -O bitcoin-${BITCOIN_VER}-x86_64-linux-gnu.tar.gz https://bitcoin.org/bin/bitcoin-core-${BITCOIN_VER}/bitcoin-${BITCOIN_VER}-x86_64-linux-gnu.tar.gz

RUN myhash=$(sha256sum "bitcoin-${BITCOIN_VER}-x86_64-linux-gnu.tar.gz" | cut -d' ' -f1); \
    if [ "$myhash" = "$BITCOIN_SHASUM" ] ; \
        then echo "checksum ok"; \
        else echo "checksum failed for bitcoin-${BITCOIN_VER}-x86_64-linux-gnu.tar.gz"; exit 255 ; \
    fi
RUN tar -xvzf bitcoin-${BITCOIN_VER}-x86_64-linux-gnu.tar.gz
RUN install -C -m 755 -o root -g root --backup=off bitcoin-${BITCOIN_FOLDER_VER}/bin/* /usr/local/bin/
RUN rm bitcoin-${BITCOIN_VER}-x86_64-linux-gnu.tar.gz && rm -rf bitcoin-${BITCOIN_FOLDER_VER}

# Set up bitcoind dirs and files
RUN mkdir -p /root/.bitcoin/
COPY bitcoin.conf /root/.bitcoin/
COPY start.sh /usr/local/bin/start.sh
RUN chmod a+x /usr/local/bin/start.sh

EXPOSE 8332 8333 18332 18333

# NOTE: Defaults to running on mainnet, specify -e TESTNET=1 to start up on testnet
ENTRYPOINT ["start.sh"]
