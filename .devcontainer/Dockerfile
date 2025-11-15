FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
ENV ANDROID_SDK_ROOT=/opt/android-sdk
ENV PATH=$PATH:$ANDROID_SDK_ROOT/cmdline-tools/latest/bin:$ANDROID_SDK_ROOT/platform-tools:$ANDROID_SDK_ROOT/emulator

# basic deps
RUN apt-get update && apt-get install -y --no-install-recommends \
    openjdk-17-jdk-headless wget unzip git curl python3 bash ca-certificates build-essential

# install android command line tools
RUN mkdir -p /opt/android-sdk/cmdline-tools \
 && cd /tmp \
 && wget -q https://dl.google.com/android/repository/commandlinetools-linux-10125470_latest.zip -O cmdline.zip \
 && mkdir -p /opt/android-sdk/cmdline-tools/latest \
 && unzip -q cmdline.zip -d /opt/android-sdk/cmdline-tools/latest \
 && rm cmdline.zip

# accept licenses non-interactively
RUN yes | /opt/android-sdk/cmdline-tools/latest/bin/sdkmanager --sdk_root=${ANDROID_SDK_ROOT} --licenses || true

# install required SDK packages (adjust api/platform-tools versions as needed)
RUN /opt/android-sdk/cmdline-tools/latest/bin/sdkmanager --sdk_root=${ANDROID_SDK_ROOT} \
    "platform-tools" "platforms;android-33" "build-tools;33.0.2" "ndk;25.1.8937393"

WORKDIR /workspace
