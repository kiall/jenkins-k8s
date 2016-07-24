FROM jenkinsci/jnlp-slave

# Install java8
RUN apt-get install -y software-properties-common && add-apt-repository -y ppa:webupd8team/java && apt-get update
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get install -y oracle-java8-installer

# Install Deps
RUN dpkg --add-architecture i386 && apt-get update && apt-get install -y --force-yes expect git wget libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5 lib32z1 python curl

# Install Android SDK
RUN cd /opt && wget -o android-sdk.tgz --quiet http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz && tar xzf android-sdk.tgz && rm -f android-sdk.tgz && chown -R root:root android-sdk-linux

# Setup environment
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools

# Install sdk elements
COPY tools /opt/tools
ENV PATH ${PATH}:/opt/tools
RUN ["/opt/tools/android-accept-licenses.sh", "android update sdk --all --force --no-ui --filter tools,platform-tools,build-tools-24.0.0,android-24,extra-google-google_play_services,extra-google-m2repository,extra-android-m2repository,sys-img-x86-android-tv-24"]

# Cleaning
RUN apt-get clean