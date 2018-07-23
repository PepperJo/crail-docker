FROM crail_base:latest
RUN apt-get install -y --no-install-recommends \
    autoconf autotools-dev automake libtool make g++ \
    librdmacm-dev libibverbs-dev ibverbs-providers

RUN cd && git clone https://github.com/zrlio/disni.git
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
RUN cd ~/disni/libdisni && ./autoprepare.sh && ./configure --with-jdk=$JAVA_HOME && make && make install
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib

COPY ./crail-env.sh $CRAIL_HOME/conf
COPY ./crail-site.conf $CRAIL_HOME/conf
COPY ./core-site.xml $CRAIL_HOME/conf
