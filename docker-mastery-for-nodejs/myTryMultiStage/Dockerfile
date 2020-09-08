# base stage (production base)
FROM node:10-slim as base

ENV NODE_ENV=production

EXPOSE 3000

# RUN apt-get update && apt-get install -y vim

WORKDIR /node

COPY package.json package-lock*.json ./

RUN npm install --only=production && npm cache clean --force


# stage2 (development stage)
FROM base as dev

ENV NODE_ENV=development

ENV PATH /node/node_modules/.bin:$PATH

WORKDIR /node

RUN npm install --only=development

WORKDIR /node/app

CMD ["nodemon", "./bin/www", "--inspect=0.0.0.0:9229"]
# CMD ["/node/node_modules/nodemon/bin/nodemon.js", "./bin/www --inspect=0.0.0.0:9229"]

# stage3 base as source
# this stage start from the first one and skip the 2 last
# allow us to copy the source code only once
FROM base as source

WORKDIR /node/app

COPY . .


# stage4 
FROM source as test

ENV NODE_ENV=development

ENV PATH=/node/node_modules/.bin:$PATH

COPY --from=dev /node/node_modules /node/node_modules

RUN eslint .

# run unit test as part of the build
RUN npm test

CMD ["npm","test"]


# stage5
FROM source as prod

CMD ["node", "./bin/www"]





