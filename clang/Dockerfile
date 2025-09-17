# syntax=docker/dockerfile:1.4
FROM ubuntu:24.04

ARG PYTHON_VERSION=3.13.7

# Install dependencies
RUN apt-get update && \
    apt-get install --no-install-recommends --yes \
        build-essential \
        ca-certificates \
        clang \
        clang-format \
        clang-tidy \
        cmake \
        curl \
        git \
        libbz2-dev \
        libffi-dev \
        liblzma-dev \
        libncursesw5-dev \
        libreadline-dev \
        libsqlite3-dev \
        libssl-dev \
        libxml2-dev \
        libxmlsec1-dev \
        make \
        sudo \
        tk-dev \
        xz-utils \
        zlib1g-dev && \
    rm -rf /var/lib/apt/lists/*

# Create a 'conan' user with passwordless sudo
RUN useradd --create-home --shell /bin/bash conan
COPY --chmod=0440 sudoers.d/conan /etc/sudoers.d/conan

USER conan
WORKDIR /home/conan

# Install pyenv
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN curl --fail --silent --show-error --location https://pyenv.run | bash
SHELL ["/bin/sh", "-c"]

ENV PYENV_ROOT="/home/conan/.pyenv"
ENV PATH="$PYENV_ROOT/bin:$PATH"

# hadolint ignore=SC2016
RUN echo 'eval "$(pyenv init - bash)"' >> .bashrc && \
    echo 'eval "$(pyenv virtualenv-init -)"' >> .bashrc

# Set default C and C++ compilers to clang
ENV CC=clang
ENV CXX=clang++

# Install Python and Conan
# hadolint ignore=DL3013
RUN eval "$(pyenv init -)" && \
    eval "$(pyenv virtualenv-init -)" && \
    pyenv install ${PYTHON_VERSION} && \
    pyenv virtualenv ${PYTHON_VERSION} conan && \
    pyenv global conan && \
    pip install --no-cache-dir conan cmakelang cpplint ruff && \
    conan profile detect
