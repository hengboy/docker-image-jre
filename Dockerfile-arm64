
FROM ubuntu:20.04

ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

RUN apt-get update \
    && apt-get install -y --no-install-recommends tzdata curl ca-certificates fontconfig locales \
    && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen en_US.UTF-8 \
    && rm -rf /var/lib/apt/lists/*

ENV JAVA_VERSION jdk11u

RUN set -eux; \
    ARCH="$(dpkg --print-architecture)"; \
    case "${ARCH}" in \
       aarch64|arm64) \
         ESUM='d3a33fb03cc59b834f0ce54aed5c788341693ab68cf0652b2a2a519aedf3eb36'; \
         BINARY_URL='https://github.com/AdoptOpenJDK/openjdk11-binaries/releases/download/jdk11u-2021-05-07-07-34/OpenJDK11U-jre_aarch64_linux_hotspot_2021-05-07-07-34.tar.gz'; \
         ;; \
       armhf|armv7l) \
         ESUM='56b013ef040c1ed1924039190bf6b8357ce233d8aa6c4fc9e87c121b5edc6694'; \
         BINARY_URL='https://github.com/AdoptOpenJDK/openjdk11-binaries/releases/download/jdk11u-2021-05-07-07-34/OpenJDK11U-jre_arm_linux_hotspot_2021-05-07-07-34.tar.gz'; \
         ;; \
       ppc64el|ppc64le) \
         ESUM='74ec88e54c1451dbb7ea5ee587f8a4c21ae4256d17d95c97163863844db688e5'; \
         BINARY_URL='https://github.com/AdoptOpenJDK/openjdk11-binaries/releases/download/jdk11u-2021-05-07-07-34/OpenJDK11U-jre_ppc64le_linux_hotspot_2021-05-07-07-34.tar.gz'; \
         ;; \
       s390x) \
         ESUM='af9425047022d30dfed4b889d613a2c1c272e6f6f1dc407fb34ec3073beee53d'; \
         BINARY_URL='https://github.com/AdoptOpenJDK/openjdk11-binaries/releases/download/jdk11u-2021-05-07-07-34/OpenJDK11U-jre_s390x_linux_hotspot_2021-05-07-07-34.tar.gz'; \
         ;; \
       amd64|x86_64) \
         ESUM='17f7b43930d7b020c7635bb134900821e82220a19f7de763d16fa430785e5bc6'; \
         BINARY_URL='https://github.com/AdoptOpenJDK/openjdk11-binaries/releases/download/jdk11u-2021-05-07-07-34/OpenJDK11U-jre_x64_linux_hotspot_2021-05-07-07-34.tar.gz'; \
         ;; \
       *) \
         echo "Unsupported arch: ${ARCH}"; \
         exit 1; \
         ;; \
    esac; \
    curl -LfsSo /tmp/openjdk.tar.gz ${BINARY_URL}; \
    echo "${ESUM} */tmp/openjdk.tar.gz" | sha256sum -c -; \
    mkdir -p /opt/java/openjdk; \
    cd /opt/java/openjdk; \
    tar -xf /tmp/openjdk.tar.gz --strip-components=1; \
    rm -rf /tmp/openjdk.tar.gz;

ENV JAVA_HOME=/opt/java/openjdk \
    PATH="/opt/java/openjdk/bin:$PATH"