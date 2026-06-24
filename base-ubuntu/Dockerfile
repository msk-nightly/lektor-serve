# Base image
FROM ubuntu:latest

# Install dependencies
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y upgrade && DEBIAN_FRONTEND="noninteractive" TZ="Etc/UTC" apt-get install -y --no-install-recommends tzdata &&\
    apt-get install -y imagemagick ffmpeg \
    && rm -rf /var/lib/apt/lists/*

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1

# Set the working directory inside the container
WORKDIR /site

# Set permissions for the working directory
RUN chown -R ubuntu:ubuntu /site

# Switch to the non-root user
USER ubuntu

ENV VIRTUAL_ENV=/site/venv
RUN python3 -m venv $VIRTUAL_ENV && \
    . /site/venv/bin/activate && \
    pip install --upgrade --no-cache-dir pip && \
    pip install --no-cache-dir -U lektor
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

EXPOSE 8888
