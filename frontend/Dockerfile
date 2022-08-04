# syntax=docker/dockerfile:1

FROM node:13.8.0-stretch-slim

EXPOSE 3000

WORKDIR /app

EXPOSE 80:3000

COPY package.json package.json
COPY package-lock.json package-lock.json

RUN npm install

COPY . .

RUN npm run build 

CMD [ "npm", "start"]
