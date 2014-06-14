FROM magicvisionlab/mvllinux-base
MAINTAINER ueck@net-labs.de
ENV DEBIAN_FRONTEND noninteractive

# enable ubuntu multiverse
RUN echo deb http://archive.ubuntu.com/ubuntu trusty multiverse >> /etc/apt/sources.list && \
    echo deb-src http://archive.ubuntu.com/ubuntu trusty multiverse >> /etc/apt/sources.list && \
    echo deb http://security.ubuntu.com/ubuntu trusty-security multiverse >> /etc/apt/sources.list && \
    echo deb-src http://security.ubuntu.com/ubuntu trusty-security multiverse >> /etc/apt/sources.list && \
    apt-get update

# install x-windows subsystem
RUN apt-get -y --force-yes install x-window-system && \
    apt-get install -y binutils && \
    apt-get install -y pkg-config && \
    apt-get install -y x11vnc && \
    apt-get install -y mesa-utils && \
    apt-get install -y libgtk2.0-0 && \
    apt-get install -y twm

RUN apt-get install -y nvidia-331
#RUN nvidia-xconfig -a --use-display-device=None --enable-all-gpus --virtual=1280x1024

# install basic packages for magicvisionlab gui development
RUN apt-get install -y \
    cmake-gui \
    libopencv-dev \
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
    coriander \
    libv4l-dev \
    qv4l2 \
    v4l2ucp \
    v4l-conf \
    libglade2-0 \
    libglademm-2.4-1c2a \
    libgtkmm-2.4-1c2a \
    libgtkglextmm-x11-1.2-dev

RUN apt-get install -y \
    nvidia-cg-dev \
    nvidia-cuda-dev \
    nvidia-cuda-gdb \
    nvidia-cuda-toolkit \
    nvidia-opencl-dev \
    libthrust-dev

