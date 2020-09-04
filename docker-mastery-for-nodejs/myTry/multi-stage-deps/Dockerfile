## Stage 1 (production base)
# This gets our prod dependencies installed and out of the way
FROM node:10-alpine as base

EXPOSE 3000

ENV NODE_ENV=production

WORKDIR /node

COPY package*.json ./

RUN npm install ci \
	&& npm cache clean --force



FROM base as dev

ENV NODE_ENV=development

ENV PATH=/node/node_modules/.bin:$PATH

WORKDIR /node

RUN npm install --only:development

WORKDIR /node/app

CMD ["nodemon", "./bin/www", "--inspect=0.0.0.0:9229"]



FROM base as prod

WORKDIR /node/app	

COPY . .

CMD ["node", "./bin/www"]

