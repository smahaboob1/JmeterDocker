# Use Java 11 JDK Oracle Linux
FROM openjdk:11-jdk-oracle
MAINTAINER Shareef
# Set the JMeter version you want to use
ARG JMETER_VERSION="5.1.1"
# Set JMeter related environment variables
ENV JMETER_HOME /opt/apache-jmeter-${JMETER_VERSION}
ENV JMETER_BIN ${JMETER_HOME}/bin
ENV JMETER_DOWNLOAD_URL https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz
# Set default values for allocation of system resources (memory) which will be used by JMeter
ENV Xms 256m
ENV Xmx 512m
ENV MaxMetaspaceSize 1024m
# Change timezone to local time
ENV TZ="America/Los_Angeles"
RUN export TZ=$TZ
# Install jmeter
RUN yum -y install curl \
&&  yum -y install wget \
&& mkdir -p /tmp/dependencies \
&& curl -L --silent ${JMETER_DOWNLOAD_URL} >  /tmp/dependencies/apache-jmeter-${JMETER_VERSION}.tgz \
&& mkdir -p /opt \
&& tar -xzf /tmp/dependencies/apache-jmeter-${JMETER_VERSION}.tgz -C /opt \
&& rm -rf /tmp/dependencies \
&& cd /tmp \
# Set JMeter home
ENV PATH $PATH:$JMETER_BIN
# copy our entrypoint
# RUN  wget https://jmeter-plugins.org/get/
COPY entrypoint.sh /opt/
COPY jmeter-plugins-casutg-2.9.jar ${JMETER_HOME}/lib/ext
COPY jmeter-plugins-filterresults-2.2.jar ${JMETER_HOME}/lib/ext
COPY jmeter-plugins-json-2.7.jar ${JMETER_HOME}/lib/ext
COPY jmeter-plugins-manager-1.3.jar ${JMETER_HOME}/lib/ext
COPY jmeter-plugins-synthesis-2.2.jar ${JMETER_HOME}/lib/ext
RUN chmod +x ./opt/entrypoint.sh
# Run command to allocate the default system resources to JMeter at 'docker run'
ENTRYPOINT ["/opt/entrypoint.sh"]
