### Build Stage
FROM node:16.16.0-alpine3.15 AS ionic

# Set the working directory
WORKDIR /usr/src/app

# Install Ionic CLI globally
RUN npm install -g @ionic/cli@7.2.0

# Copy package.json and package-lock.json first for caching layer optimization
COPY package*.json ./

# Install dependencies
RUN npm ci --force

# Copy the rest of the application source code
COPY . .

# Build the Ionic application
RUN ionic build

### Run Stage
FROM nginx:alpine

# Copy the build output from the build stage to the Nginx html directory
COPY --from=ionic /usr/src/app/www /usr/share/nginx/html
