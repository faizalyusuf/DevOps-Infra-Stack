FROM ubuntu:16.04

# Install packages
RUN apt-get update -y && apt-get install -y apt-utils && apt-get upgrade && apt-get install -y wget && apt-get install -y openjdk-8-jdk && apt-get install unzip

# Install AndroidSDK

# Download sdk tools
RUN wget https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip
RUN unzip -d /opt/Android/ sdk-tools-linux-3859397.zip && rm sdk-tools-linux-3859397.zip

# Set PATH for SDK and sdkmanager
ENV PATH=$PATH:/opt/Android/tools
ENV PATH=$PATH:/opt/Android/tools/bin

# Download packages
RUN echo y | sdkmanager "platform-tools"
RUN echo y | sdkmanager "platforms;android-26"

# Set PATH for ANDROID_HOME
ENV ANDROID_HOME=/opt/Android

