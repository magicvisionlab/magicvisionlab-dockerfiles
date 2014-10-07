FROM magicvisionlab/ubuntu32:14.04
MAINTAINER ueck@net-labs.de
ENV DEBIAN_FRONTEND noninteractive
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle

# add localized apt sources.list
ADD conf/sources.list /etc/apt/sources.list

RUN apt-get update; \
    apt-get install -y apt-utils net-tools

# LOCAL BUILD ONLY - USE AptProxy
#RUN echo "Use Localhost as AptProxy http://"`netstat -nr | grep '^0\.0\.0\.0' | awk '{print $2}'`":3142"
#RUN echo 'Acquire::http { Proxy "http://'`netstat -nr | grep '^0\.0\.0\.0' | awk '{print $2}'`':3142"; };' | tee /etc/apt/apt.conf.d/02proxy

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

RUN add-apt-repository -y ppa:mc3man/trusty-media

RUN pip --no-input --exists-action=w install --upgrade pip

# Fake a fuse install, since build cannot run in privileged mode
RUN apt-get install libfuse2 && \
    cd /tmp && apt-get download fuse && \
    cd /tmp && dpkg-deb -x fuse_* . && \
    cd /tmp && dpkg-deb -e fuse_* && \
    cd /tmp && rm fuse_*.deb && \
    cd /tmp && echo -en '#!/bin/bash\nexit 0\n' > DEBIAN/postinst && \
    cd /tmp && dpkg-deb -b . /fuse.deb && \
    cd /tmp && dpkg -i /fuse.deb && \
    rm /fuse.deb
# end hack

# install oracle java 1.7
WORKDIR /tmp
RUN wget --progress=bar --no-check-certificate -O /tmp/jdk-7u60-linux-i586.tar.gz \
         --header "Cookie: oraclelicense=a" http://download.oracle.com/otn-pub/java/jdk/7u60-b19/jdk-7u60-linux-i586.tar.gz && \
    tar xzf /tmp/jdk-7u60-linux-i586.tar.gz && \
    mkdir -p /usr/lib/jvm/java-7-oracle && \
    mv jdk1.7.0_60/jre /usr/lib/jvm/java-7-oracle/jre && \
    mv jdk1.7.0_60/lib /usr/lib/jvm/java-7-oracle/lib && \
    mv jdk1.7.0_60/include /usr/lib/jvm/java-7-oracle/include && \
    mv jdk1.7.0_60/bin /usr/lib/jvm/java-7-oracle/bin && \
    mv jdk1.7.0_60/man /usr/lib/jvm/java-7-oracle/man && \
    mv jdk1.7.0_60/db /usr/lib/jvm/java-7-oracle/db && \
    rm -rf jdk1.7.0_60 && rm /tmp/jdk-7u60-linux-i586.tar.gz && \
    chown root:root -R /usr/lib/jvm/java-7-oracle && \
    update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-7-oracle/jre/bin/java 1 && \
    update-alternatives --set java /usr/lib/jvm/java-7-oracle/jre/bin/java
# end oracle java installation

# install basic packages for magicvisionlab development
RUN apt-get install --force-yes -y \
    libzmq-dev \
    libboost-all-dev \
    libatlas-dev \
    libavcodec-dev \
    libavformat-dev \
    libblas-dev \
    libbullet-dev \
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
    libreadline-dev \
    libtbb-dev \
    zlib1g-dev \
    vim \
    vim-scripts \
    wget \
    ctags \
    gdb \
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
    ant \
    checkinstall \
    cmake \
    pkg-config \
    yasm \
    libjasper-dev \
    libswscale-dev \
    libdc1394-22-dev \
    libxine-dev \
    libgstreamer0.10-dev \
    libgstreamer-plugins-base0.10-dev \
    libv4l-dev \
    python-numpy \
    libtbb-dev \
    libgtk2.0-dev \
    libfaac-dev \
    libmp3lame-dev \
    libopencore-amrnb-dev \
    libopencore-amrwb-dev \
    libtheora-dev \
    libvorbis-dev \
    libxvidcore-dev \
    x264 \
    v4l-utils \
    x-window-system \
    binutils \
    x11vnc \
    mesa-utils \
    libgtk2.0-0 \
    twm \
    cmake-gui \
    libqt4-dev \
    libqt4-dev-bin \
    libqt4-opengl-dev \
    libqt4-qt3support \
    libqt4-sql-sqlite \
    libqtwebkit-dev \
    freeglut3-dev \
    libftgl-dev \
    libfreetype6-dev \
    libglew-dev \
    libglfw-dev \
    libwxgtk3.0-dev \
    libmotif-dev \
    libx11-dev \
    libxft-dev \
    libxi-dev \
    libxslt1-dev \
    mesa-common-dev \
    qtbase5-dev \
    qtbase5-dev-tools \
    libxmu-dev \
    libglade2-0 \
    libglademm-2.4-1c2a \
    libgtkmm-2.4-1c2a \
    libgtkglextmm-x11-1.2-dev


# CLEANUP LOCAL PROXY
RUN rm -f /etc/apt/apt.conf.d/02proxy
