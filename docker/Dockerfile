FROM alpine:3.19 AS repo

USER root

RUN apk add --no-cache bash ca-certificates git openssh-client

RUN mkdir -p -m 0700 /root/.ssh && ssh-keyscan "github.com" >> /root/.ssh/known_hosts

RUN --mount=type=secret,id=my_ssh_key,dst=/root/.ssh/id_rsa \
    mkdir -p /app && cd app \
    && ssh -T git@github.com || true \
    && git clone git@github.com:cfallwell/pacman.git

WORKDIR /app

# Keep the container running
ENTRYPOINT ["tail", "-f", "/dev/null"]


FROM node:boron AS build

LABEL owner="Colin Fallwell" owner_email="212790803+cfallwell@users.noreply.github.com"

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Clone game source code
COPY --from=0 /app/pacman /usr/src/app

# Set envornment variables
ENV OTEL_SERVICE_NAME='pacman'
ENV OTEL_EXPORTER_OTLP_ENDPOINT=splunk1.falhalla.intra:4317
ENV OTEL_RESOURCE_ATTRIBUTES='deployment.environment=dev,service.version=1.0'
ENV SPLUNK_PROFILER_ENABLED='true'
ENV SPLUNK_PROFILER_MEMORY_ENABLED='true'
ENV SPLUNK_METRICS_ENABLED='true'

# Install app dependencies
RUN npm install

# Expose port 8280
EXPOSE 8280

# Run container
CMD ["npm", "start"]
