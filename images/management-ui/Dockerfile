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
FROM graviteeio/httpd:latest
MAINTAINER Gravitee Team <http://gravitee.io>

ARG GRAVITEEIO_VERSION=0

RUN echo 'root:gravitee' | chpasswd
RUN groupadd gravitee && useradd -s /bin/bash -m -g gravitee gravitee
RUN echo 'gravitee:gravitee' |chpasswd

COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod u+x /usr/local/bin/entrypoint.sh

RUN wget  https://bintray.com/artifact/download/gravitee-io/release/${GRAVITEEIO_VERSION}/graviteeio-management-ui-${GRAVITEEIO_VERSION}.zip \
    && zip -FFv graviteeio-management-ui-${GRAVITEEIO_VERSION}.zip --out graviteeio-management-ui-${GRAVITEEIO_VERSION}.fixed.zip \
    && unzip graviteeio-management-ui-${GRAVITEEIO_VERSION}.fixed.zip \
    && rm graviteeio-management-ui-${GRAVITEEIO_VERSION}.fixed.zip \
    && mv graviteeio-management-ui-${GRAVITEEIO_VERSION}/* /var/www/html \
    && rmdir graviteeio-management-ui-${GRAVITEEIO_VERSION}

ENV MGMT_API_URL http://localhost/management/
RUN cp /var/www/html/constants.js /var/www/html/constants.js.template

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD ["/usr/sbin/httpd", "-DFOREGROUND"]
