FROM  hub.ywwl.com/template/openjdk-8
ARG JAR_FILE
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN apk add ffmpeg ffmpeg-libs ffmpeg-dev gcc make libgcc g++ 
ADD silk-v3-decoder /opt/silk-v3-decoder
ENTRYPOINT exec echo 0