# ubuntu is a base image
FROM ubuntu

# installing nodejs
RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_18.x | bash -
RUN apt-get update -y
RUN apt-get install -y nodejs

# copying required files/folders from local machine to container
COPY package.json package.json
COPY package-lock.json package-lock.json

RUN npm install
# COPY server.js server.js
COPY . .

ENTRYPOINT [ "node", "server.js" ]

# FROM node

# COPY package.json package.json
# COPY package-lock.json package-lock.json
# COPY server.js server.js

# RUN npm install

# ENTRYPOINT [ "node", "server.js" ]
