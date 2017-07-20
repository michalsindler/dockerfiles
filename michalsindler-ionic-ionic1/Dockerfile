FROM     ubuntu:14.04.4
MAINTAINER  Michal Sindler docker [at] sindler [dot] net

ENV DEBIAN_FRONTEND=noninteractive \
    ANDROID_HOME=/opt/android-sdk-linux \
    NODE_VERSION=6.10.0 \
    NPM_VERSION=3.10.10 \
    IONIC_VERSION=1.* \
    CORDOVA_VERSION=6.5.0 \
    GRADLE_VERSION=4.0

# Prerequisities
RUN apt-get update && \
    apt-get install -y git wget curl unzip ruby && \

# NodeJS
    curl --retry 3 -SLO "http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" && \
    tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 && \
    rm "node-v$NODE_VERSION-linux-x64.tar.gz" && \
# Npm
    npm install -g npm@"$NPM_VERSION" && \
# Cordova
    npm install -g cordova@"$CORDOVA_VERSION" ionic@"$IONIC_VERSION" && \
    npm cache clear && \
# Sass
    gem install sass && \

# Java
    apt-get update && apt-get install -y -q python-software-properties software-properties-common  && \
    add-apt-repository ppa:webupd8team/java -y && \
    echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get update && apt-get -y install oracle-java8-installer && \

# Android
## Prerequisities
    echo ANDROID_HOME="${ANDROID_HOME}" >> /etc/environment && \
    dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -y --force-yes expect ant wget libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5 lib32z1 qemu-kvm kmod && \
    apt-get clean && \
    apt-get autoclean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
## SDK
    cd /opt && \
    wget --output-document=android-sdk.tgz --quiet http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz && \
    tar xzf android-sdk.tgz && \
    rm -f android-sdk.tgz && \
    chown -R root. /opt && \

# Gradle
    mkdir -p /opt/gradle && \
    wget --output-document="gradle-$GRADLE_VERSION.bin.zip" --quiet "https://services.gradle.org/distributions/gradle-$GRADLE_VERSION-bin.zip" && \
    unzip -d /opt/gradle "gradle-$GRADLE_VERSION.bin.zip" && \
    ls "/opt/gradle/gradle-$GRADLE_VERSION"

# Setup environment
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:/opt/tools:/opt/gradle/gradle-4.0/bin

# Android Licenses
COPY tools /opt/tools
RUN ["/opt/tools/android-accept-licenses.sh", "android update sdk --all --no-ui --filter platform-tools,tools,build-tools-23.0.2,android-23,android-25,extra-android-support,extra-android-m2repository,extra-google-m2repository"]
RUN unzip ${ANDROID_HOME}/temp/*.zip -d ${ANDROID_HOME}

WORKDIR myApp
EXPOSE 8100 35729 5037
CMD ["ionic", "info"]
