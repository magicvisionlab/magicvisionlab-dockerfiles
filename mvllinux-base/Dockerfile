FROM ubuntu:14.04
MAINTAINER ueck@net-labs.de
ENV DEBIAN_FRONTEND noninteractive
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle

# enable ubuntu extras
RUN echo deb http://extras.ubuntu.com/ubuntu trusty main >> /etc/apt/sources.list;\
    echo deb-src http://extras.ubuntu.com/ubuntu trusty main >> /etc/apt/sources.list;\
    apt-get update;


## install ubuntu packages
RUN apt-get update; \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3E5C1192; \
    apt-get update; apt-get upgrade -y


# install basic development tools
RUN apt-get install -y \
    software-properties-common \
    python-software-properties \
    python2.7-dev \
    python-distribute \
    python-pip \
    build-essential \
    devscripts \
    supervisor \
    wget

RUN pip --no-input --exists-action=w install --upgrade pip

# Fake a fuse install, since build cannot run in privileged mode
RUN apt-get install libfuse2
RUN cd /tmp ; apt-get download fuse
RUN cd /tmp ; dpkg-deb -x fuse_* .
RUN cd /tmp ; dpkg-deb -e fuse_*
RUN cd /tmp ; rm fuse_*.deb
RUN cd /tmp ; echo -en '#!/bin/bash\nexit 0\n' > DEBIAN/postinst
RUN cd /tmp ; dpkg-deb -b . /fuse.deb
RUN cd /tmp ; dpkg -i /fuse.deb
# end hack

# install oracle java 1.7
WORKDIR /tmp
RUN wget --progress=bar --no-check-certificate -O /tmp/jdk-7u60-linux-x64.tar.gz --header "Cookie: oraclelicense=a" http://download.oracle.com/otn-pub/java/jdk/7u60-b19/jdk-7u60-linux-x64.tar.gz

RUN tar xzf /tmp/jdk-7u60-linux-x64.tar.gz
RUN mkdir -p /usr/lib/jvm/java-7-oracle
RUN mv jdk1.7.0_60/jre /usr/lib/jvm/java-7-oracle/jre
RUN mv jdk1.7.0_60/lib /usr/lib/jvm/java-7-oracle/lib
RUN mv jdk1.7.0_60/include /usr/lib/jvm/java-7-oracle/include
RUN mv jdk1.7.0_60/bin /usr/lib/jvm/java-7-oracle/bin
RUN mv jdk1.7.0_60/man /usr/lib/jvm/java-7-oracle/man
RUN mv jdk1.7.0_60/db /usr/lib/jvm/java-7-oracle/db

RUN rm -rf jdk1.7.0_60 && rm /tmp/jdk-7u60-linux-x64.tar.gz
RUN chown root:root -R /usr/lib/jvm/java-7-oracle
RUN update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-7-oracle/jre/bin/java 1
RUN update-alternatives --set java /usr/lib/jvm/java-7-oracle/jre/bin/java
# end oracle java installation

# install basic packages for magicvisionlab development
RUN apt-get install -y \
    libzmq-dev \
    libboost-all-dev \
    libatlas-dev \
    libavcodec-dev \
    libavformat-dev \
    libblas-dev \
    libbullet-dev \
    libdc1394-22-dev \
    libflann-dev \
    libeigen3-dev \
    libexpat1-dev \
    libfreeimage-dev \
    libhdf5-dev \
    libjpeg-dev \
    liblapack-dev \
    libprotobuf-dev \
    libmsgpack-dev \
    libqhull-dev \
    libraw1394-dev \
    libreadline-dev \
    libtbb-dev \
    libusb-dev \
    zlib1g-dev \
    vim \
    vim-scripts \
    wget \
    ctags \
    gpm \
    git \
    rsync \
    git-man \
    subversion \
    bzr \
    mercurial \
    binutils-gold \
    cmake \
    cmake-curses-gui \
    python-numpy \
    python-scipy \
    swig \
    ant



