FROM ubuntu:24.04

# Install dependencies
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

# Set default C and C++ compilers to clang
ENV CC=clang
ENV CXX=clang++
ENV PATH="/home/ubuntu/.local/bin:$PATH"

# Install Python and Conan
# hadolint ignore=DL3013
RUN pipx install --pip-args='--no-cache-dir' conan cmakelang cpplint ruff && \
    conan profile detect
