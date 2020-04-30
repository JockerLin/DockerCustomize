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

RUN \
  apt-get update && \
  apt-get -y install wget unzip

WORKDIR /

# Set Language Env
RUN \
  apt-get update && \
  apt-get install -y locales locales-all && \
  rm -rf /var/lib/apt/lists/* && \
  locale-gen en_HK.UTF-8
ENV LANG en_HK.UTF-8
ENV LANGUAGE en_HK:en
ENV LC_ALL en_HK.UTF-8

# OPENCV (change to the source)
RUN \
  pip install opencv-python==3.4.0.12
# RUN pip install numpy

# OPENCV
# question: I build succeed, but I can't find cv2*.so in site-packages.
# ENV OPENCV_VERSION="3.4.0"
# COPY ${OPENCV_VERSION}.zip /${OPENCV_VERSION}.zip
# # RUN wget https://github.com/opencv/opencv/archive/${OPENCV_VERSION}.zip
# RUN unzip ${OPENCV_VERSION}.zip \
# && mkdir /opencv-${OPENCV_VERSION}/build \
# && cd /opencv-${OPENCV_VERSION}/build \
# && cmake -DBUILD_TIFF=ON \
#   -DBUILD_opencv_java=OFF \
#   -DBUILD_opencv_python3=ON \
#   -DBUILD_SHARED_LIBS=ON \
#   -DWITH_CUDA=OFF \
#   -DWITH_OPENGL=ON \
#   -DWITH_OPENCL=ON \
#   -DWITH_IPP=ON \
#   -DWITH_TBB=ON \
#   -DWITH_EIGEN=ON \
#   -DWITH_V4L=ON \
#   -DBUILD_TESTS=OFF \
#   -DBUILD_PERF_TESTS=OFF \
#   -DINSTALL_PYTHON_EXAMPLES=ON \
#   -DCMAKE_BUILD_TYPE=RELEASE \
#   -DCMAKE_INSTALL_PREFIX=/user/local \
#   -DPYTHON_EXECUTABLE=/usr/bin/python3 \
#   -DPYTHON_INCLUDE_DIR=/usr/local/include/python3 \
#   -DPYTHON_PACKAGES_PATH=/usr/local/lib/python3.6/site-packages \
#   .. \
# && make -j4 \
# && make install && ldconfig

# RUN rm /${OPENCV_VERSION}.zip \
# && rm -r /opencv-${OPENCV_VERSION}

# RUN ln -s \
#   /usr/local/lib/python3.6/site-packages/cv2.cpython-36m-x86_64-linux-gnu.so \
#   /usr/local/lib/python3.6/site-packages/cv2.so

# restore work dir
WORKDIR /