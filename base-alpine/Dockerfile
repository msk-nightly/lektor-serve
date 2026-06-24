# Base image
FROM alpine:latest

# Install dependencies
RUN apk --no-cache --update-cache upgrade && \
    apk --no-cache add tzdata python3 py3-pip imagemagick ffmpeg

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1

# Set the working directory inside the container
WORKDIR /site

# Create a non-root user
RUN addgroup lektor && \
    adduser -G lektor -D lektor && \
    chown -R lektor:lektor /site

# Switch to the non-root user
USER lektor

ENV VIRTUAL_ENV=/site/venv
RUN python3 -m venv $VIRTUAL_ENV && \
    . /site/venv/bin/activate && \
    pip install --upgrade --no-cache-dir pip && \
    pip install --no-cache-dir -U lektor
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

EXPOSE 8888
