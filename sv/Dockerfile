FROM ubuntu

RUN cd ~
RUN apt-get update && apt-get install -y build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils
RUN apt-get install -y libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev libboost-test-dev libboost-thread-dev
RUN apt-get install -y libdb-dev libdb++-dev
RUN apt-get install -y libzmq3-dev
RUN apt-get install -y wget python3

RUN wget https://download.bitcoinsv.io/bitcoinsv/1.0.1/bitcoin-sv-1.0.1.tar.gz && tar -xf bitcoin-sv-1.0.1.tar.gz
RUN cd bitcoin-sv-1.0.1 && ./autogen.sh && ./configure && make && make install
RUN mkdir .bitcoin
COPY bitcoin/bitcoin.conf .bitcoin

CMD ["bitcoind", "--conf=/home/root/.bitcoin/bitcoin.conf"]

EXPOSE 18332