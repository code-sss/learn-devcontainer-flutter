# Use Flutter's pre-configured Docker image with Android SDK from GitHub Container Registry
FROM ghcr.io/cirruslabs/flutter:stable AS base

# Create the vscode user with home directory and sudo privileges
RUN sudo useradd -m -s /bin/bash vscode && \
    sudo usermod -aG sudo vscode && \
    sudo echo 'vscode ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/vscode

# Install dependencies for Android Emulator and NVIDIA GPU support
RUN sudo apt-get update && \
    sudo apt-get install -y \
    software-properties-common && \
    sudo add-apt-repository ppa:graphics-drivers/ppa && \
    sudo apt-get update && \
    sudo apt-get install -y \
    qemu-kvm \
    libvirt-daemon-system \
    libvirt-clients \
    bridge-utils \
    virt-manager \
    lib32stdc++6 \
    lib32z1 \
    lib32ncurses6 \
    lib32gcc-s1 \
    unzip \
    curl \
    git \
    sudo \
    libglu1-mesa \
    nvidia-driver-550 \
    nvidia-cuda-toolkit \
    && sudo apt-get clean

# Optional: Accept Android SDK licenses
RUN flutter doctor --android-licenses

# Set the working directory to /workspaces (common for VSCode containers)
WORKDIR /workspaces

# Set vscode user as the default user
USER vscode