FROM node:12-alpine as builder
WORKDIR /yapi
RUN apk add --no-cache wget python2 make
ENV VERSION=1.9.2
RUN wget https://github.com/YMFE/yapi/archive/refs/tags/v1.9.5.zip
RUN unzip v1.9.5.zip && mv yapi-1.9.5 vendors
RUN cd /yapi/vendors && cp config_example.json ../config.json && npm install --production --registry https://registry.npm.taobao.org

FROM node:12-alpine
ENV TZ="Asia/Shanghai"
WORKDIR /yapi/vendors
COPY --from=builder /yapi/vendors /yapi/vendors
EXPOSE 3000
ENTRYPOINT ["node"]
