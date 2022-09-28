### builder
FROM mcr.microsoft.com/dotnet/sdk:5.0-focal-arm64v8 AS builder
ENV DEBIAN_FRONTEND=noninteractive

ARG OBS_VERSION=27.2.4

RUN apt-get update && apt-get -y install --no-install-recommends \
      apt-transport-https \
      software-properties-common \
           build-essential \
           checkinstall \
           cmake \
           git \
           libmbedtls-dev \
           libasound2-dev \
           libavcodec-dev \
           libavdevice-dev \
           libavfilter-dev \
           libavformat-dev \
           libavutil-dev \
           libcurl4-openssl-dev \
           libfontconfig1-dev \
           libfreetype6-dev \
           libgl1-mesa-dev \
           libjack-jackd2-dev \
           libjansson-dev \
           libluajit-5.1-dev \
           libpulse-dev \
           libqt5x11extras5-dev \
           libspeexdsp-dev  \
           libswresample-dev  \
           libswscale-dev \
           libudev-dev \
           libv4l-dev \
           libvlc-dev \
           libx11-dev \
           libx264-dev \
           libxcb-shm0-dev \
           libxcb-xinerama0-dev \
           libxcomposite-dev \
           libxinerama-dev \
           pkg-config  \
           python3-dev \
           qtbase5-dev \
           libqt5svg5-dev \
           swig \
           libxcb-randr0-dev \
           libxcb-xfixes0-dev  \
           libxcb1-dev \
           libx11-xcb-dev \
           \
           libwayland-dev \
           libxkbcommon-dev \
           libpci-dev \
           qtbase5-private-dev \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/*

RUN git clone -b ${OBS_VERSION} --recursive https://github.com/obsproject/obs-studio.git
RUN mkdir obs-studio/build && \
    cd obs-studio/build && \
    cmake -DENABLE_WAYLAND=OFF -DENABLE_PIPEWIRE=OFF -DBUILD_BROWSER=OFF -DUNIX_STRUCTURE=1 -DCMAKE_INSTALL_PREFIX=/usr .. && \
    make && \
    mkdir /package && \
    checkinstall --install=no --default --pkgname=obs --pkgversion=${OBS_VERSION} --pakdir=/package

RUN ls -l /package
