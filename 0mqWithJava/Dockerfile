FROM ubuntu:17.04

MAINTAINER Chiradip Mandal <chiradip@chiradip.com>

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y git build-essential libtool autoconf automake pkg-config unzip libkrb5-dev
RUN cd /tmp && git clone git://github.com/jedisct1/libsodium.git && cd libsodium && git checkout e2a30a && ./autogen.sh && ./configure && make check && make install && ldconfig

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository ppa:git-core/ppa
RUN apt-get update

RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer


# Define working directory.
WORKDIR /data

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

RUN cd /tmp && git clone --depth 1 git://github.com/zeromq/libzmq.git && cd libzmq && ./autogen.sh && ./configure && make
# RUN cd /tmp/libzmq && make check
RUN cd /tmp/libzmq && make install && ldconfig
RUN cd /tmp && git clone --depth 1 git://github.com/zeromq/jzmq.git && cd jzmq/jzmq-jni && ./autogen.sh && ./configure && make
RUN cd /tmp/jzmq/jzmq-jni && make install && ldconfig
RUN rm /tmp/* -rf
