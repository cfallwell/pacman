FROM node:boron

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Clone game source code
RUN git clone https://github.com/cfallwell/pacman.git .

# Install app dependencies
RUN npm install

# Expose port 8080
EXPOSE 8280

# Setup OpenTelemetry
ENV OTEL_SERVICE_NAME='pacman'
ENV OTEL_RESOURCE_ATTRIBUTES='deployment.environment=dev,service.version=1.0'
ENV OTEL_ENVER_OTLP_ENDPOINT='http://localhost:4318'
ENV SPLUNK_PROFILER_MEMORY_ENABLED='true'
ENV SPLUNK_METRICS_ENABLED='true'
ENV SPLUNK_AUTOMATIC_LOG_COLLECTION='true'

# Run container
CMD ["npm", "start"]