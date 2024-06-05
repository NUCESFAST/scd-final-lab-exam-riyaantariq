# Use the official Node.js image for build stage
FROM node:14 AS build

# Set the working directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the app for production with minification
RUN npm run build

# Use nginx to serve the static files
FROM nginx:alpine
COPY --from=build /usr/src/app/build /usr/share/nginx/html

# Expose the port nginx runs on
EXPOSE 1101

# No need to specify CMD, nginx image has default command to run
