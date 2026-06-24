# Base image
FROM ubuntu:25.10

# Install dependencies
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y upgrade && DEBIAN_FRONTEND="noninteractive" TZ="Etc/UTC" apt-get install -y --no-install-recommends tzdata &&\
    apt-get install -y sudo pipx imagemagick ffmpeg \
    && rm -rf /var/lib/apt/lists/*

# Create a sudoer non-root user
RUN passwd -d root && \
    passwd -d ubuntu

# Set the working directory inside the container
WORKDIR /site

# Set permissions for the working directory
RUN chown -R ubuntu:ubuntu /site

# Switch to the non-root user
USER ubuntu

# Ensure the presence of pipx in the PATH variable
RUN /bin/bash -c "pipx ensurepath && source ~/.bashrc"

# Install lektor
RUN pipx install lektor
