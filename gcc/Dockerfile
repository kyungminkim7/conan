FROM conanio/gcc11-ubuntu18.04

ARG CONAN_VERSION=2.11.0

RUN pip install --no-cache-dir --upgrade conan==${CONAN_VERSION} && \
    conan profile detect && \
    conan remote update conancenter --url="https://center2.conan.io"

USER root

RUN apt-get update && \
    apt-get install --no-install-recommends --yes \
        libfontenc-dev \
        libgl-dev \
        libice-dev \
        libsm-dev \
        libxaw7-dev \
        libxcb-composite0-dev \
        libxcb-cursor-dev \
        libxcb-ewmh-dev \
        libxcb-icccm4-dev \
        libxcb-image0-dev \
        libxcb-keysyms1-dev \
        libxcb-render-util0-dev \
        libxcb-res0-dev \
        libxcb-util-dev \
        libxcb-util0-dev \
        libxcb-xinerama0-dev \
        libxcb-xkb-dev \
        libxcomposite-dev \
        libxcursor-dev \
        libxi-dev \
        libxinerama-dev \
        libxkbfile-dev \
        libxmu-dev \
        libxmuu-dev \
        libxpm-dev \
        libxrandr-dev \
        libxrender-dev \
        libxres-dev \
        libxss-dev \
        libxt-dev \
        libxtst-dev \
        libxv-dev \
        uuid-dev \
        xkb-data && \
    rm -rf /var/lib/apt/lists/*

USER conan
