FROM alpine as builder
LABEL maintainer="contact@graviteesource.com"

ARG GRAVITEEIO_VERSION=0
ENV GRAVITEEIO_HOME /opt/graviteeio-gateway

RUN apk add --update zip unzip netcat-openbsd wget

RUN wget https://download.gravitee.io/graviteeio-apim/distributions/graviteeio-full-${GRAVITEEIO_VERSION}.zip --no-check-certificate -P /tmp/ \
    && unzip /tmp/graviteeio-full-${GRAVITEEIO_VERSION}.zip -d /tmp/ \
    && mv /tmp/graviteeio-full-${GRAVITEEIO_VERSION}/graviteeio-gateway* ${GRAVITEEIO_HOME} \
    && rm -rf /tmp/*
    
FROM aibar/gravitee-java:11
LABEL maintainer="contact@graviteesource.com"

ENV GRAVITEEIO_HOME /opt/graviteeio-gateway

COPY --from=builder ${GRAVITEEIO_HOME} ${GRAVITEEIO_HOME}

RUN chgrp -R 0 ${GRAVITEEIO_HOME} && \
    chmod -R g=u ${GRAVITEEIO_HOME}

WORKDIR ${GRAVITEEIO_HOME}

EXPOSE 8082
CMD ["./bin/gravitee"]
