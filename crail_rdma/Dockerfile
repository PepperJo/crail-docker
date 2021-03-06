# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.)

FROM crail:latest
MAINTAINER Apache Crail <dev@crail.apache.org>

RUN echo "Crail-$LOG_COMMIT install rdma libraries and autotools" && \
    apt-get install -y --no-install-recommends \
    autoconf autotools-dev automake libtool make g++ \
    librdmacm-dev libibverbs-dev ibverbs-providers

RUN echo "Crail-$LOG_COMMIT clone and build disni native library" && \
    cd && git clone https://github.com/zrlio/disni.git && \
    cd ~/disni/libdisni && \
    ./autoprepare.sh && \
    ./configure --with-jdk=$JAVA_HOME && \
    make && make install
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib

COPY ./crail-site.conf $CRAIL_HOME/conf
