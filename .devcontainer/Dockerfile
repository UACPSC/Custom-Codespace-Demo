# Use the C++ base image
FROM mcr.microsoft.com/devcontainers/cpp
ARG TARGETPLATFORM

# Update and install dependencies
RUN apt-get update && apt-get install --no-install-recommends -y \
    gh \
    asciinema \
    ninja-build \
    libarchive-dev \
    hyperfine \
    autoconf \
    autotools-dev \
    graphviz \
    libxml2-utils \
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

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Set the timezone to New York time
RUN apt-get update && \
    apt-get install -yq tzdata && \
    ln -fs /usr/share/zoneinfo/America/New_York /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata

# Create a new group localbin
RUN groupadd localbin

# Add 'vscode' user to 'mygroup'
RUN usermod -a -G localbin vscode

# Change group ownership of /usr/local/bin to 'mygroup'
# And set the group write permission
RUN chown root:localbin /usr/local/bin
RUN chmod 775 /usr/local/bin

# Install srcML
COPY srcml_1.0.0-1_ubuntu22.04_x86_64.deb srcml_1.0.0-1_ubuntu22.04_aarch64.deb ./
RUN case "${TARGETPLATFORM}" in \
        "linux/amd64") \
            SRCML_PACKAGE="srcml_1.0.0-1_ubuntu22.04_x86_64.deb" ;; \
        "linux/arm64") \
            SRCML_PACKAGE="srcml_1.0.0-1_ubuntu22.04_aarch64.deb" ;; \
    esac && \
    apt-get update && \
    apt-get install ./${SRCML_PACKAGE} -y && \
    rm -rf /var/lib/apt/lists/* && \
    rm ./*.deb

# Install concern
COPY parsingConcerns /usr/local/bin/concerns
RUN chmod a+x /usr/local/bin/concerns
