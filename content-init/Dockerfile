# This is the base image that can be used
FROM node:alpine AS base
WORKDIR /usr/src/app
ENV MONGODB_CONNECTION=mongodb://mongo:27017/contentdb

FROM node:argon AS build
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json /usr/src/app/
RUN npm install

# Bundle app source
COPY . /usr/src/app

FROM base as final
WORKDIR /usr/src/app
COPY --from=build /usr/src/app .
CMD [ "npm", "start" ] 