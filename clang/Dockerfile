FROM ubuntu:24.04

RUN apt-get update && \
    apt-get install --no-install-recommends --yes \
        clang \
        clang-format \
        clang-tidy \
        cmake \
        make \
        pipx \
        sudo && \
    rm -rf /var/lib/apt/lists/*

COPY --chmod=0440 sudoers.d/ubuntu /etc/sudoers.d/

USER ubuntu
WORKDIR /home/ubuntu

ENV CC=clang
ENV CXX=clang++

ENV PATH="/home/ubuntu/.local/bin:$PATH"

# hadolint ignore=DL3013
RUN pipx install --pip-args='--no-cache-dir' conan cmakelang cpplint ruff && \
    conan profile detect
