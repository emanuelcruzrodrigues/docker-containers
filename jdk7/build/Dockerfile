FROM ubuntu:latest
MAINTAINER Emanuel Cruz Rodrigues <emanuelcruzrodrigues@gmail.com>

ENV JAVA_HOME=/opt/jdk
ENV PATH="${PATH}:${JAVA_HOME}/bin"

COPY java-linux-x64.tar.gz /temp/

RUN \
mkdir $JAVA_HOME \
&& tar -xf /temp/java-linux-x64.tar.gz --directory=$JAVA_HOME \
&& rm -rf /temp

