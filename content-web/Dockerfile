# Dockerfile for content-web
# This is the base image that can be used
FROM node:dubnium-alpine AS base
RUN apk -U add curl
WORKDIR /usr/src/app
ENV PORT=80
EXPOSE 80
ENV CONTENT_API_URL=http://api:3001

FROM node:dubnium AS build
RUN npm install -g @angular/cli@~8.3.4

WORKDIR /usr/src/app

# Install app dependencies
COPY package.json /usr/src/app/
RUN npm install

# Bundle app source
COPY . /usr/src/app
RUN ng build 

FROM base as final
WORKDIR /usr/src/app
COPY --from=build /usr/src/app .
CMD [ "node", "app.js" ]