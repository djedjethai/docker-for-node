FROM node:8 as prod
ENV NODE_ENV=production

RUN apt-get update\
    && apt-get install tini\
    && apt-get install -y graphicsmagick;

WORKDIR /app

COPY package.json package-*lock.json

RUN npm install --only:production && npm cache clean --force
RUN npm install winston-transport

COPY ..

CMD ["node", "index.js"]


FROM prod as test
ENV NODE_ENV=development
CMD ["npm", "test"]




