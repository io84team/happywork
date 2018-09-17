FROM node:latest
LABEL name="node:pdftk"

USER root

RUN apt-get update && apt-get install -y \
    pdftk \
    --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*

EXPOSE 8080
WORKDIR /data
