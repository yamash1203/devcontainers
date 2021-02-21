FROM debian:buster

ARG USERNAME=vscode
ARG USER_UID=1000
ARG SBT_VERSION=1.4.7

ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64

RUN apt update \
    && apt install -y sudo wget git openjdk-11-jdk openjdk-11-source openjdk-11-doc \
    && useradd -s /bin/bash --uid ${USER_UID} -m ${USERNAME} \
    && echo "${USERNAME} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME} \
    && wget --no-verbose --output-document=/tmp/sbt-$SBT_VERSION.deb https://dl.bintray.com/sbt/debian/sbt-$SBT_VERSION.deb \
    && dpkg -i /tmp/sbt-$SBT_VERSION.deb \
    && rm -f /tmp/sbt-$SBT_VERSION.deb

# sbt cannot execute on root directory
USER ${USERNAME}
WORKDIR /home/${USERNAME}
CMD ["sbt"]
