FROM ubuntu:24.04

ARG PYTHON_VERSION=3.13.7

# Install dependencies
RUN apt-get update && \
    apt-get install --no-install-recommends --yes \
        clang \
        clang-format \
        clang-tidy \
        cmake \
        make \
        pipx && \
    rm -rf /var/lib/apt/lists/*

# Create a 'conan' user with passwordless sudo
RUN useradd --create-home --shell /bin/bash conan
COPY --chmod=0440 sudoers.d/conan /etc/sudoers.d/conan

USER conan
WORKDIR /home/conan

# Set default C and C++ compilers to clang
ENV CC=clang
ENV CXX=clang++
ENV PATH="/home/conan/.local/bin:$PATH"

# Install Python and Conan
# hadolint ignore=DL3013
RUN pipx install conan cmakelang cpplint ruff && \
    conan profile detect
