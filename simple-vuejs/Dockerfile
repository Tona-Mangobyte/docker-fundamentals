# Use an official Node.js runtime as the base image
FROM node:18-alpine
# Set the working directory inside the container
WORKDIR /var/www/vuejs
# Copy package.json to the working directory
COPY package.json /var/www/vuejs/
COPY yarn.lock /var/www/vuejs/
COPY node_modules /var/www/vuejs/
# Copy the rest of the application source code
COPY . /var/www/vuejs
# Install application dependencies
#RUN yarn install
# Install Vue Service
#RUN yarn add @vue/cli-service
# debug 
RUN ls -la /var/www/vuejs
# list dependencies
RUN ls -la /var/www/vuejs/node_modules
# Expose a port that the application listens on
EXPOSE 8080
# Define the command to run the application when the container starts
CMD ["yarn", "serve"]