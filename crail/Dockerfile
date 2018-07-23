FROM ubuntu:18.04
ARG GIT_COMMIT=master
RUN apt-get update && apt-get install --no-install-recommends -y \
    git \
    openjdk-8-jdk-headless \
    gettext-base
RUN apt-get install --no-install-recommends -y maven
RUN git clone https://github.com/apache/incubator-crail.git
WORKDIR /incubator-crail
RUN git checkout ${GIT_COMMIT}
RUN mvn -DskipTests package

ENV CRAIL_HOME /incubator-crail/assembly/target/crail-1.0-bin
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
ENV PATH ${PATH}:${JAVA_HOME}/bin:${CRAIL_HOME}/bin

RUN sed -i '$ienvsubst < $CRAIL_HOME/conf/core-site.xml > $CRAIL_HOME/conf/core-site.xml' $CRAIL_HOME/bin/crail

ENV NAMENODE_HOST=localhost
ENV NAMENODE_PORT=9060
ENV INTERFACE=eth0
ENV DATAPATH=/dev/hugepages/data
ENV STORAGELIMIT=1073741824
ENV CACHEPATH=/dev/hugepages/cache
ENV CACHELIMIT=1073741824

COPY ./crail-env.sh $CRAIL_HOME/conf
COPY ./core-site.xml $CRAIL_HOME/conf
COPY ./crail-site.conf $CRAIL_HOME/conf
