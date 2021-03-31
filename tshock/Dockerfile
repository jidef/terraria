FROM alpine:3.11.6 AS base

#TShock URL
ENV TSHOCKURL="https://github.com/Pryaxis/TShock/releases/download/v4.4.0-pre15/TShock4.4.0_Pre15_Terraria1.4.1.2.zip"

RUN apk add --update-cache \
    unzip
ADD $TSHOCKURL /tshock.zip
RUN unzip /tshock.zip -d /tshock && \
    TSHOCKNAME=$(ls /tshock) && \
    mv /tshock/$TSHOCKNAME/* /tshock/ && \
    rm tshock.zip && \
    chmod +x /tshock/TerrariaServer.exe

FROM mono:6.8.0.96-slim

RUN apt-get update -y && \
    apt-get install -y nuget && \
    rm -rf /var/lib/apt/lists/* /tmp/*

COPY --from=base /tshock/ /tshock/

RUN echo "mono --server --gc=sgen -O=all /tshock/TerrariaServer.exe \
    -configpath /root \
    -worldselectpath /root \
    -logpath /root/logs \
    $@" >> /tshock/START

VOLUME ["/root"]
EXPOSE 7777
WORKDIR /tshock
ENTRYPOINT [ "/bin/sh", "START"]
LABEL maintainer="github.com/jidef"


