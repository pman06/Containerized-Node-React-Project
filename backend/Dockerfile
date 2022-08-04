# syntax=docker/dockerfile:1

FROM node:13.8.0-stretch-slim

EXPOSE 3000

WORKDIR /app

EXPOSE 3000

COPY package.json package.json
COPY package-lock.json package-lock.json

RUN npm install
RUN npm install pm2

COPY . .

CMD [ "pm2", "start", "npm", "--", "start"]
