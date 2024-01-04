FROM gradle:7.4-jdk17

RUN apt-get update && apt-get install -y \
		zip \
		curl \
        xz-utils

# Install Android SDK Tools
ENV ANDROID_HOME "/home/jochim28/android-sdk"
ENV ANDROID_SDK_ROOT $ANDROID_HOME
ENV CMDLINE_TOOLS_ROOT "${ANDROID_HOME}/cmdline-tools/latest/bin"
ENV ADB_INSTALL_TIMEOUT 120
ENV PATH "${ANDROID_HOME}/emulator:${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/platform-tools/bin:${PATH}"
# You can find the latest command line tools here: https://developer.android.com/studio#command-line-tools-only
RUN SDK_TOOLS_URL="https://dl.google.com/android/repository/commandlinetools-linux-10406996_latest.zip" && \
	mkdir -p ${ANDROID_HOME}/cmdline-tools && \
	mkdir ${ANDROID_HOME}/platforms && \
	mkdir ${ANDROID_HOME}/ndk && \
	wget -O /tmp/cmdline-tools.zip -t 5 "${SDK_TOOLS_URL}" && \
	unzip -q /tmp/cmdline-tools.zip -d ${ANDROID_HOME}/cmdline-tools && \
	rm /tmp/cmdline-tools.zip && \
	mv ${ANDROID_HOME}/cmdline-tools/cmdline-tools ${ANDROID_HOME}/cmdline-tools/latest

RUN echo y | ${CMDLINE_TOOLS_ROOT}/sdkmanager "tools" && \
	echo y | ${CMDLINE_TOOLS_ROOT}/sdkmanager "platform-tools" && \
    echo y | ${CMDLINE_TOOLS_ROOT}/sdkmanager "build-tools;34.0.0" && \
    echo y | ${CMDLINE_TOOLS_ROOT}/sdkmanager "build-tools;30.0.3" && \
	echo y | ${CMDLINE_TOOLS_ROOT}/sdkmanager "platforms;android-30" && \
    echo y | ${CMDLINE_TOOLS_ROOT}/sdkmanager "platforms;android-31" && \
    echo y | ${CMDLINE_TOOLS_ROOT}/sdkmanager "platforms;android-32" && \
    echo y | ${CMDLINE_TOOLS_ROOT}/sdkmanager "platforms;android-33"

# Install some useful packages
RUN echo y | ${CMDLINE_TOOLS_ROOT}/sdkmanager "extras;android;m2repository" && \
	echo y | ${CMDLINE_TOOLS_ROOT}/sdkmanager "extras;google;m2repository"

# Install Flutter Version Manager
ENV FLUTTER_VERSION=3.10.2
ENV FLUTTER_HOME "/home/jochim28/flutter"
ENV PATH $PATH:${FLUTTER_HOME}/bin
RUN FLUTTER_URL="https://mirrors.cloud.tencent.com/flutter/flutter_infra/releases/stable/linux/flutter_linux_${FLUTTER_VERSION}-stable.tar.xz" && \
	wget -O /tmp/flutter.tar.xz -t 5 "${FLUTTER_URL}" && \
	tar -xvf /tmp/flutter.tar.xz -C /home/jochim28 && \
	git config --global --add safe.directory "*" && \
	rm /tmp/flutter.tar.xz