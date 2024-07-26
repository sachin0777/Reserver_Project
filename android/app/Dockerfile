# Use an official Ubuntu as a parent image
FROM ubuntu:18.04

# Set non-interactive installation mode
ENV DEBIAN_FRONTEND=noninteractive

# Prerequisites
RUN apt update && apt install -y \
    curl \
    git \
    unzip \
    xz-utils \
    zip \
    libglu1-mesa \
    openjdk-8-jdk \
    wget \
    lib32stdc++6 \
    lib32z1 \
    libbz2-1.0 \
    libncurses5 \
    libncursesw5 \
    libstdc++6 \
    && rm -rf /var/lib/apt/lists/*

# Set up a new user and switch to it
RUN useradd -ms /bin/bash developer
USER developer
WORKDIR /home/developer

# Prepare Android SDK directories and system variables
RUN mkdir -p Android/sdk
ENV ANDROID_SDK_ROOT=/home/developer/Android/sdk
RUN mkdir -p .android && touch .android/repositories.cfg

# Set up Android SDK
RUN wget -qO sdk-tools.zip https://dl.google.com/android/repository/commandlinetools-linux-8512546_latest.zip
RUN unzip -q sdk-tools.zip -d Android/sdk && rm sdk-tools.zip
RUN cd Android/sdk/cmdline-tools/bin && yes | ./sdkmanager --licenses
RUN cd Android/sdk/cmdline-tools/bin && ./sdkmanager "build-tools;29.0.2" "platform-tools" "platforms;android-29" "sources;android-29"

# Download and set up Flutter SDK
RUN git clone https://github.com/flutter/flutter.git -b stable
ENV PATH="$PATH:/home/developer/flutter/bin"

# Run basic Flutter checks
RUN flutter doctor --android-licenses
RUN flutter doctor

# Expose port for the Flutter web server (optional, based on use case)
EXPOSE 8000

# Default command (can be overridden)
CMD ["bash"]
