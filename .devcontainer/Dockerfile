# Use the C++ base image
FROM mcr.microsoft.com/devcontainers/cpp

# Update and install dependencies
RUN apt-get update && apt-get install --no-install-recommends -y \
    gh \
    asciinema \
    ninja-build \
    && rm -rf /var/lib/apt/lists/*

# Install cmake
RUN apt-get update && \
    apt-get install gpg wget --no-install-recommends -y && \
    wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | gpg --dearmor - | sudo tee /usr/share/keyrings/kitware-archive-keyring.gpg >/dev/null && \
    echo 'deb [signed-by=/usr/share/keyrings/kitware-archive-keyring.gpg] https://apt.kitware.com/ubuntu/ jammy main' | sudo tee /etc/apt/sources.list.d/kitware.list >/dev/null && \
    apt-get update && \
    rm /usr/share/keyrings/kitware-archive-keyring.gpg && \
    apt-get install kitware-archive-keyring && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install cmake --no-install-recommends -y && \
    rm -rf /var/lib/apt/lists/*
