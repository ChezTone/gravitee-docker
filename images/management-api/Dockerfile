#-------------------------------------------------------------------------------
# Copyright (C) 2015 The Gravitee team (http://gravitee.io)
#    Licensed under the Apache License, Version 2.0 (the "License");
#    you may not use this file except in compliance with the License.
#    You may obtain a copy of the License at
#            http://www.apache.org/licenses/LICENSE-2.0
#    Unless required by applicable law or agreed to in writing, software
#    distributed under the License is distributed on an "AS IS" BASIS,
#    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#    See the License for the specific language governing permissions and
#    limitations under the License.
#-------------------------------------------------------------------------------
FROM graviteeio/java:8
MAINTAINER Gravitee Team <http://gravitee.io>

ARG GRAVITEEIO_VERSION=0

RUN echo 'root:gravitee' | chpasswd
RUN groupadd gravitee && useradd -s /bin/bash -m -g gravitee gravitee
RUN echo 'gravitee:gravitee' |chpasswd

USER gravitee
WORKDIR /home/gravitee

RUN wget https://bintray.com/artifact/download/gravitee-io/release/${GRAVITEEIO_VERSION}/graviteeio-management-api-${GRAVITEEIO_VERSION}.zip \
    && zip -FFv graviteeio-management-api-${GRAVITEEIO_VERSION}.zip --out graviteeio-management-api-${GRAVITEEIO_VERSION}.fixed.zip \
    && unzip graviteeio-management-api-${GRAVITEEIO_VERSION}.fixed.zip \
    && rm graviteeio-management-api-${GRAVITEEIO_VERSION}.fixed.zip

ENV GRAVITEEIO_HOME /home/gravitee/graviteeio-management-api-${GRAVITEEIO_VERSION}
WORKDIR ${GRAVITEEIO_HOME}

ENV GRAVITEEIO_MONGODB_HOST localhost
ENV GRAVITEEIO_MONGODB_PORT 27017
ENV GRAVITEEIO_ELASTIC_HOST localhost
ENV GRAVITEEIO_ELASTIC_PORT 9300

EXPOSE 8083
VOLUME ["/home/gravitee/log"]
CMD ["./bin/gravitee"]
