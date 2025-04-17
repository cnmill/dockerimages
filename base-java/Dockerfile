FROM  openjdk:8u212-jdk-alpine
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN apk add tzdata && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone
RUN apk add --update font-adobe-100dpi ttf-dejavu fontconfig bash busybox-extras curl tini libc6-compat linux-pam krb5 krb5-libs ffmpeg ffmpeg-libs ffmpeg-dev
#ADD US_export_policy.jar /usr/lib/jvm/java-1.8-openjdk/jre/lib/security/US_export_policy.jar
#ADD local_policy.jar /usr/lib/jvm/java-1.8-openjdk/jre/lib/security/local_policy.jar
ADD libWeWorkFinanceSdk_Java.so /usr/lib/libWeWorkFinanceSdk_Java.so
ENV LANG=zh_CN.UFT-8 LC_ALL=zh_CN.UFT-8
COPY --from=hengyunabc/arthas:latest /opt/arthas /arthas
# takin
#ADD agent-opensource /takin-agent
# skywalking
ADD agent /app/agent
ADD entrypoint.sh /entrypoint.sh
WORKDIR /
CMD [ "/bin/sh -c set -x " ]
