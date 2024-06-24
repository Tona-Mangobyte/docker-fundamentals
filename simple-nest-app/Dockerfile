FROM node:18-alpine

WORKDIR /var/www/server

COPY package.json /var/www/server/
COPY yarn.lock /var/www/server/

# Copy the rest of the application source code
COPY . /var/www/server

# Install application dependencies
RUN yarn install

# Expose a port that the application listens on
EXPOSE 3000
# Define the command to run the application when the container starts
CMD ["yarn", "dev"]