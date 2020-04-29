FROM ubuntu:16.04

# change apt source
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak
COPY ./sources.list /etc/apt/sources.list

# Install System Deps
RUN \
  apt-get update && \
  apt-get -f install && \
  apt-get install --fix-missing

RUN \
  apt-get -y install build-essential git zlib1g-dev checkinstall && \
  apt-get -y install g++ cmake && \
  apt-get -y install libdmtx0a python-jpype && \
  apt-get -y install liblapack-dev liblapacke-dev libatlas-dev libatlas-base-dev libblas-dev libeigen3-dev && \
  apt-get -y install libzbar-dev libsqlite3-dev && \
  apt-get -y install libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev && \
  apt-get -y install libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev libv4l-dev && \
  apt-get -y install libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev && \
  rm -rf /var/lib/apt/lists/*

ENV LD_LIBRARY_PATH /usr/local/lib

# Install Python3.6
COPY ./Python-3.6.4.tar.xz /Python-3.6.4.tar.xz
RUN \
  tar xf Python-3.6.4.tar.xz && \
  cd Python-3.6.4 && \
  ./configure --disable-shared --enable-loadable-sqlite-extensions && \
  make -j4 && \
  make install && \
  ln -sf /usr/local/bin/python3.6 /usr/bin/python && \
  rm -rf /Python-3.6.4.tar.xz /Python-3.6.4

# pip(fail offen when internet is bad)
# COPY ./get-pip.py /get-pip.py
# RUN \
#   python get-pip.py && \
#   ln -sf /usr/local/bin/pip3 /usr/local/bin/pip

# pip(online from aliyun)
RUN \
  apt-get update && \
  apt-get -y install python-pip

WORKDIR /root
RUN mkdir .pip
WORKDIR /root/.pip/
COPY ./pip.conf pip.conf

# opencv
RUN \
  pip install opencv-python==3.4.0.12

# restore work dir
WORKDIR /