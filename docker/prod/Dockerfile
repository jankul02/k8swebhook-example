FROM golang:1.17.1-alpine as build-stage

RUN apk --no-cache add \
    g++ \
    git \
    make \
    bash

ARG VERSION
ENV VERSION=${VERSION}

WORKDIR /src
COPY . .
RUN ./scripts/build/build.sh

# Final image.
FROM alpine:latest
RUN apk --no-cache add \
    ca-certificates
COPY --from=build-stage /src/bin/k8s-webhook-example /usr/local/bin/k8s-webhook-example
ENTRYPOINT ["/usr/local/bin/k8s-webhook-example"]