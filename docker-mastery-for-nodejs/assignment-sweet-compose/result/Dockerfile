FROM node:8.16-alpine

ENV NODE_ENV=development 

RUN apk add --no-cache tini \
	&& apk add --update bash \
	&& apk add vim

WORKDIR /node

# RUN npm install -g nodemon\
# COPY package*.json /app/

COPY package*.json /node/
RUN mkdir app && chown -R node:node .

# USER node // do not work 
RUN npm install \
 && npm install nodemon --save-dev \
 && npm ls \
 && npm cache clean --force 
# && mv /app/node_modules /node_modules

WORKDIR /node/app

COPY . /app

ENV PORT 80
EXPOSE 80

ENTRYPOINT ["/sbin/tini", "--"]

CMD ["node", "server.js"]
