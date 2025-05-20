FROM mcr.microsoft.com/azure-functions/python:4-python3.12

ARG HOST_GID=1000
ARG HOST_UID=1000

USER root

RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    azure-functions-core-tools-4 \
    git \
  && \
  rm -rf /var/lib/apt/lists/*


RUN if ! getent group "${HOST_GID}" > /dev/null; then \
      groupadd -g "${HOST_GID}" sitegroup; \
    else \
      echo "GID ${HOST_GID} already exist, skipping groupadd"; \
    fi \
    && useradd --uid ${HOST_UID} --gid ${HOST_GID} --create-home site


RUN mkdir -p /home/site/.azurefunctions /home/site/data \
 && chown -R ${HOST_UID}:${HOST_GID} /home/site


USER site
ENV HOME=/home/site
WORKDIR /home/site/wwwroot

