FROM emanuel/jdk7:latest
MAINTAINER Emanuel Cruz Rodrigues <emanuelcruzrodrigues@gmail.com>

RUN \
apt-get update \
&& export DEBIAN_FRONTEND=noninteractive \
&& ln -fs /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime \
&& apt-get install -y tzdata \
&& apt-get install -y wget \
&& wget http://download.jboss.org/jbossas/7.1/jboss-as-7.1.1.Final/jboss-as-7.1.1.Final.tar.gz -P /tmp \
&& mkdir /opt/jboss \
&& tar -xf /tmp/jboss.tar.gz --directory=/opt/jboss/ \
&& rm -f /tmp/jboss.tar.gz

COPY standalone.conf /opt/jboss/jboss-as-7.1.1.Final/bin/standalone.conf
COPY standalone.xml /opt/jboss/jboss-as-7.1.1.Final/standalone/configuration/standalone.xml

# Expose ports   
EXPOSE 8080 8787

ENTRYPOINT sed -i -- 's/DS_NAME/'"$DS_NAME"'/g' /opt/jboss/jboss-as-7.1.1.Final/standalone/configuration/standalone.xml \
&& sed -i -- 's/DB_DRIVER/'"$DB_DRIVER"'/g' /opt/jboss/jboss-as-7.1.1.Final/standalone/configuration/standalone.xml \
&& sed -i -- 's/DB_USERNAME/'"$DB_USERNAME"'/g' /opt/jboss/jboss-as-7.1.1.Final/standalone/configuration/standalone.xml \
&& sed -i -- 's/DB_PASSWORD/'"$DB_PASSWORD"'/g' /opt/jboss/jboss-as-7.1.1.Final/standalone/configuration/standalone.xml \
&& sed -i -- 's#DB_CONNECTION_URL#'"$DB_CONNECTION_URL"'#g' /opt/jboss/jboss-as-7.1.1.Final/standalone/configuration/standalone.xml \
&& ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
&& dpkg-reconfigure --frontend noninteractive tzdata \
&& /opt/jboss/jboss-as-7.1.1.Final/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0

