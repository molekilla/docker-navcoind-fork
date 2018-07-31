FROM ubuntu:16.04

LABEL maintainer.0="Paul Sanderson"

#NavCoin settings
ARG NAVCOIN_VERSION=4.2.1
ARG NAV_CHK=1500674cc0c9f31a5369c21dd59b3cccdbf25c5db8a04f728967029552725d3e
ARG NAV_PKG=navcoin-${NAVCOIN_VERSION}-x86_64-linux-gnu.tar.gz

#install the libs needed
RUN apt-get update -y
RUN apt-get install ntp wget -y
RUN apt-get install libcurl4-openssl-dev -y

WORKDIR /tmp

#download NavCoin and check it
RUN mkdir -p ${NAVCOIN_VERSION}
RUN wget "https://github.com/NAVCoin/navcoin-core/releases/download/${NAVCOIN_VERSION}/${NAV_PKG}"
RUN echo "${NAV_CHK}  ${NAV_PKG}" | sha256sum -c
RUN tar -xzf ${NAV_PKG}

# move navcoind
WORKDIR /tmp/navcoin-${NAVCOIN_VERSION}/bin
RUN cp navcoind /bin/navcoind
RUN cp navcoin-cli /bin/navcoin-cli

WORKDIR /
VOLUME [ "/root/.navcoin4" ]
#cleanup
RUN rm -rf /tmp/*
EXPOSE 44444 44440 44445
ENTRYPOINT ["/bin/bash", "-c"]
