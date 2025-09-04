FROM node:boron

MAINTAINER Colin Fallwell <212790803+cfallwell@users.noreply.github.com>

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Clone game source code
RUN git clone git://github.com/cfallwell/pacman.git .

# Install app dependencies
RUN npm install

# Expose port 8080
EXPOSE 8080

# Run container
CMD ["npm", "start"]
