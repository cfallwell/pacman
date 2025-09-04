FROM node:boron

MAINTAINER Ivan Font <ifont@redhat.com>

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Clone game source code
RUN git clone https://github.com/cfallwell/pacman.git .

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
