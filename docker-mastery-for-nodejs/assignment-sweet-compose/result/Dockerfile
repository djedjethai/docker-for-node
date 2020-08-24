FROM node:8.16-alpine

ENV NODE_ENV=development 

WORKDIR /app

RUN apk add --update bash
# RUN npm install -g nodemon

COPY package*.json /app/
RUN npm install \
 && npm install nodemon --save-dev \
 && npm ls \
 && npm cache clean --force \
 && mv /app/node_modules /node_modules
COPY . /app

ENV PORT 80
EXPOSE 80

CMD ["node", "server.js"]
