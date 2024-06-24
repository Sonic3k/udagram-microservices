### Build
FROM node:16.16.0-alpine3.15 AS ionic  # Node.js 16.16.0 Alpine image

## Install app dependencies
RUN npm install -g @ionic/cli@7.2.0
RUN npm install -f

## Copy package.json and package-lock.json
COPY package*.json ./ 

## Create app directory
WORKDIR /usr/src/app

## Install dependencies
RUN npm ci --force

## Bundle app source
COPY . .

RUN ionic build

### Run
FROM nginx:alpine
COPY --from=ionic /usr/src/app/www /usr/share/nginx/html
