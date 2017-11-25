FROM jenkins

ENV http_proxy=${http_proxy}
ENV https_proxy=${https_proxy}

# Install Jenkins plugins
#RUN install-plugins.sh \
    # Core plugins
#    blueocean \
#    docker-workflow \
#    locale \

    # Pipeline related
#    workflow-aggregator \
#    pipeline-stage-view \

    # VCS related
#    git \
#    cloudbees-bitbucket-branch-source \
#    github-organization-folder

#Install Docker binaries
# see: https://docs.docker.com/engine/installation/binaries/
#USER root
#RUN cd \
#    && set -x \
#    && curl -fSL "https://get.docker.com/builds/Linux/x86_64/docker-latest.tgz" -o docker.tgz \
#    && tar -xzvf docker.tgz \
#    && mv docker/* /usr/local/bin/ \
#    && rmdir docker \
#    && rm docker.tgz

#RUN groupadd docker \
#    && usermod -aG docker,staff jenkins

USER jenkins

#VOLUME /var/run/docker.sock

USER root
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB

# Install Ruby.
#RUN \
#  apt-get update && \
#  apt-get install -y ruby ruby-dev ruby-bundler rubygems build-essential && \
#  rm -rf /var/lib/apt/lists/*

#RUN curl -sSL https://raw.githubusercontent.com/wayneeseguin/rvm/stable/binscripts/rvm-installer | bash -s stable --ruby

#ENV FASTLANE_VERSION=2.55.0

#RUN gem install fastlane:$FASTLANE_VERSION -NV

#Install gradle
# Install packages
RUN apt-get -y update && apt-get install -y apt-utils && apt-get -y upgrade && apt-get install -y wget openjdk-8-jdk unzip 

# Download gradle
#RUN wget https://services.gradle.org/distributions/gradle-4.1-bin.zip && mkdir /opt/gradle && unzip -d /opt/gradle gradle-4.1-bin.zip && rm gradle-4.1-bin.zip

# Set Environment variables
#ENV GRADLE_HOME=/opt/gradle/gradle-4.1/bin
#ENV PATH=$PATH:$GRADLE_HOME

#Install AndroidSDK

#Download sdk tools
RUN wget https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip

#unzip into folder
RUN unzip -o -d /opt/android-sdk-linux sdk-tools-linux-3859397.zip && rm sdk-tools-linux-3859397.zip

#set PATH
ENV PATH=$PATH:/opt/android-sdk-linux/tools
ENV PATH=$PATH:/opt/android-sdk-linux/tools/bin

#download packages

RUN echo y | sdkmanager "platform-tools"
RUN echo y | sdkmanager "platforms;android-26"
RUN echo y | sdkmanager "system-images;android-26;google_apis;x86"

#set PATH for ANDROID_HOME

ENV ANDROID_HOME /opt/android-sdk-linux

RUN echo '\
function emulator { cd "$(dirname "$(which emulator)")" && ./emulator "$@"; } \
' >> /root/.profile

RUN echo "no" | avdmanager create avd -n test --package "system-images;android-26;google_apis;x86" --tag "google_apis" --abi "x86"

ENTRYPOINT ["/bin/tini", "--", "/usr/local/bin/jenkins.sh"]
