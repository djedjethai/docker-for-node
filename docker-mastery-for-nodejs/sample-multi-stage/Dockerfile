FROM node:10-slim as prod
ENV NODE_ENV=production
EXPOSE 3000

# RUN apk add --no-cache tini work only on alpine image

# RUN apt-get update do not work
WORKDIR /node
COPY package.json package-lock*.json ./
RUN mkdir app && chown -R node:node .
USER node
RUN npm install --only=production && npm cache clean --force
WORKDIR /node/app
COPY . .
# ENTRYPOINT ["/sbin/tini", "--"]
# could do that to run a test before run the app
# RUN npm test
CMD ["node", "./bin/www"]


FROM prod as dev
ENV NODE_ENV=development
RUN npm install --only=development
CMD ["node_modules/nodemon/bin/nodemon.js", "./bin/www --inspect=0.0.0.0:9229"]


FROM dev as test
ENV NODE_ENV=development
# not good for dev testing but great for ci as it will create a new image link to the ci
CMD ["npm","test"]
