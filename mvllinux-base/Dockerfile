FROM ubuntu:14.04
MAINTAINER ueck@net-labs.de
ENV DEBIAN_FRONTEND noninteractive

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
    python-pip \
    libzmq-dev \
    python2.7-dev \
    build-essential \
    devscripts \
    supervisor \
    openssh-server \
    wget

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
    libopencv-dev \
    libboost-all-dev \
    freeglut3-dev \
    libatlas-dev \
    libavcodec-dev \
    libavformat-dev \
    libblas-dev \
    libbullet-dev \
    libdc1394-22-dev \
    libflann-dev \
    libftgl-dev \
    libfreetype6-dev \
    libglew-dev \
    libeigen3-dev \
    libexpat1-dev \
    libfreeimage-dev \
    libglfw-dev \
    libhdf5-dev \
    libjpeg-dev \
    liblapack-dev \
    libmotif-dev \
    libprotobuf-dev \
    libmsgpack-dev \
    libqhull-dev \
    libraw1394-dev \
    libreadline-dev \
    libtbb-dev \
    libusb-dev \
    libwxgtk3.0-dev \
    libx11-dev \
    libxft-dev \
    libxi-dev \
    libxslt1-dev \
    mesa-common-dev \
    qtbase5-dev \
    qtbase5-dev-tools \
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
    nvidia-cg-dev \
    nvidia-cuda-dev \
    nvidia-cuda-gdb \
    nvidia-cuda-toolkit \
    nvidia-opencl-dev \
    libthrust-dev \
    libxmu-dev \
    binutils-gold \
    cmake \
    cmake-gui


