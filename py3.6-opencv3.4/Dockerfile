FROM python:3.6

RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak
COPY ./sources.list /etc/apt/sources.list

# Install System Deps
RUN \
  apt-get update && \
  apt-get -y install build-essential git zlib1g-dev checkinstall && \
  apt-get -y install g++ cmake && \
  apt-get -y install libdmtx0a python-jpype && \
  apt-get -y install liblapack-dev liblapacke-dev libatlas-dev libatlas-base-dev libblas-dev libeigen3-dev && \
  apt-get -y install libzbar-dev libsqlite3-dev && \
  apt-get -y install libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev && \
  apt-get -y install libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev libv4l-dev && \
  apt-get -y install libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev && \
  rm -rf /var/lib/apt/lists/*

COPY ./get-pip.py /get-pip.py
RUN \
  python get-pip.py && \
  ln -sf /usr/local/bin/pip3 /usr/local/bin/pip

RUN pip install numpy
RUN pip install opencv-python==3.4.0.12
