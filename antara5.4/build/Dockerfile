FROM ubuntu:20.04
MAINTAINER Emanuel Cruz Rodrigues <emanuelcruzrodrigues@gmail.com>

ENV JAVA_HOME=/opt/jdk
ENV JBOSS_HOME=/opt/jboss
ENV PATH="${PATH}:${JAVA_HOME}/bin"

# install
RUN apt-get update
RUN apt-get install -y tzdata

#jdk 6
COPY jdk6.tar.gz /temp/

RUN \
mkdir $JAVA_HOME \
&& tar -xf /temp/jdk6.tar.gz --directory=$JAVA_HOME

# jboss
COPY jboss.tar.gz.parta* /temp/

RUN cat /temp/jboss.tar.gz.parta* > /temp/jboss.tar.gz

RUN mkdir $JBOSS_HOME \
&& tar -xf /temp/jboss.tar.gz --directory=$JBOSS_HOME \
&& rm -rf /temp

# Expose ports   
EXPOSE 8080 8787

ENTRYPOINT sed -i -- 's/DS_NAME/'"$DS_NAME"'/g' $JBOSS_HOME/standalone/configuration/standalone.xml \
&& sed -i -- 's/DB_USERNAME/'"$DB_USERNAME"'/g' $JBOSS_HOME/standalone/configuration/standalone.xml \
&& sed -i -- 's/DB_PASSWORD/'"$DB_PASSWORD"'/g' $JBOSS_HOME/standalone/configuration/standalone.xml \
&& sed -i -- 's#DB_CONNECTION_URL#'"$DB_CONNECTION_URL"'#g' $JBOSS_HOME/standalone/configuration/standalone.xml \
&& ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
&& dpkg-reconfigure --frontend noninteractive tzdata \
&& $JBOSS_HOME/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0

