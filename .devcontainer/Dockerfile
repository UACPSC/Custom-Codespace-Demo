# Use the C++ base image
FROM mcr.microsoft.com/devcontainers/cpp

# Install gh
# Update and install dependencies
RUN apt-get update && apt-get install --no-install-recommends -y \
    gh \
    && rm -rf /var/lib/apt/lists/*

# Install latest cmake
RUN curl -L "https://cmake.org/files/v3.27/cmake-3.27.7-linux-x86_64.tar.gz" | tar xz --strip-components=1 -C /usr/local/
