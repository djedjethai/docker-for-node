FROM node:8 
# as prod
# ENV NODE_ENV = production

RUN apt-get update && apt-get install -y graphicsmagick;

WORKDIR /app

COPY package.json package-lock*.json ./

RUN npm install && npm cache clean --force
RUN npm install winston-transport

COPY . .

ENV CHARCOAL_FACTOR=0.1

CMD ["node", "index.js"]


# FROM prod as test
# ENV NODE_ENV=development
# CMD ["npm", "test"]




