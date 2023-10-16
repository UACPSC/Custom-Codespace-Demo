# Use the C++ base image
FROM mcr.microsoft.com/devcontainers/cpp

# Install gh
# Update and install dependencies
RUN apt-get update && apt-get install --no-install-recommends -y \
    gh \
    asciinema \
    && rm -rf /var/lib/apt/lists/*

# Install cmake
ARG TARGETPLATFORM
RUN echo "${TARGETPLATFORM}"
RUN case "${TARGETPLATFORM}" in \
         "linux/amd64")  ARCHITECTURE="x86_64"   ;; \
         "linux/arm64")  ARCHITECTURE="aarch64"  ;; \
         "linux/arm64/v8")  ARCHITECTURE="aarch64"  ;; \
         *)  exit 1 ;; \
    esac; \
    curl --insecure -L "https://github.com/Kitware/CMake/releases/download/v3.27.7/cmake-3.27.7-linux-${ARCHITECTURE}.tar.gz" | tar xz --strip-components=1 -C /usr/local
