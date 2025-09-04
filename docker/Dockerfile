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

# Run container
CMD ["npm", "start"]