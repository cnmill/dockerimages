FROM flink:1.20.0-scala_2.12-java8

RUN rm -rf $JAVA_HOME
RUN /bin/sh -c set -eux; ARCH="$(dpkg --print-architecture)"; case "${ARCH}" in aarch64|arm64) ESUM='8c3146035b99c55ab26a2982f4b9abd2bf600582361cf9c732539f713d271faf'; BINARY_URL='https://github.com/adoptium/temurin11-binaries/releases/download/jdk-11.0.21%2B9/OpenJDK11U-jdk_aarch64_linux_hotspot_11.0.21_9.tar.gz'; ;; amd64|i386:x86-64) ESUM='60ea98daa09834fdd3162ca91ddc8d92a155ab3121204f6f643176ee0c2d0d5e'; BINARY_URL='https://github.com/adoptium/temurin11-binaries/releases/download/jdk-11.0.21%2B9/OpenJDK11U-jdk_x64_linux_hotspot_11.0.21_9.tar.gz'; ;; armhf|arm) ESUM='a64b005b84b173e294078fec34660ed3429d8c60726a5fb5c140e13b9e0c79fa'; BINARY_URL='https://github.com/adoptium/temurin11-binaries/releases/download/jdk-11.0.21%2B9/OpenJDK11U-jdk_arm_linux_hotspot_11.0.21_9.tar.gz'; ;; ppc64el|powerpc:common64) ESUM='262ff98d6d88a7c7cc522cb4ec4129491a0eb04f5b17dcca0da57cfcdcf3830d'; BINARY_URL='https://github.com/adoptium/temurin11-binaries/releases/download/jdk-11.0.21%2B9/OpenJDK11U-jdk_ppc64le_linux_hotspot_11.0.21_9.tar.gz'; ;; s390x|s390:64-bit) ESUM='bc67f79fb82c4131d9dcea32649c540a16aa380a9726306b9a67c5ec9690c492'; BINARY_URL='https://github.com/adoptium/temurin11-binaries/releases/download/jdk-11.0.21%2B9/OpenJDK11U-jdk_s390x_linux_hotspot_11.0.21_9.tar.gz'; ;; *) echo "Unsupported arch: ${ARCH}"; exit 1; ;; esac; wget --progress=dot:giga -O /tmp/openjdk.tar.gz ${BINARY_URL}; echo "${ESUM} */tmp/openjdk.tar.gz" | sha256sum -c -; mkdir -p "$JAVA_HOME"; tar --extract --file /tmp/openjdk.tar.gz --directory "$JAVA_HOME" --strip-components 1 --no-same-owner ; rm -f /tmp/openjdk.tar.gz ${JAVA_HOME}/lib/src.zip; find "$JAVA_HOME/lib" -name '*.so' -exec dirname '{}' ';' | sort -u > /etc/ld.so.conf.d/docker-openjdk.conf; ldconfig; java -Xshare:dump;

# install python3 and pip3
RUN apt-get update -y && \
apt-get install -y python3 python3-pip python3-dev && rm -rf /var/lib/apt/lists/*
RUN ln -s /usr/bin/python3 /usr/bin/python

# install PyFlink
RUN pip3 install apache-flink==1.20.0

RUN wget -P /opt/flink/lib https://repo.maven.apache.org/maven2/org/apache/flink/flink-sql-connector-kafka_2.12/1.20.0/flink-sql-connector-kafka_scala_2.12-1.20.0.jar
