ARG NODE_IMAGE=node:16.13.1-alpine

FROM $NODE_IMAGE AS base

LABEL maintainer="Fernando Koji <fernandokojidev@gmail.com>"

RUN apk update

RUN apk --no-cache add dumb-init

RUN mkdir -p /var/www/rifaisso && chown node:node /var/www/rifaisso

WORKDIR /var/www/rifaisso

USER node

RUN mkdir tmp

FROM base AS dependencies

RUN yarn install --frozen-lockfile

COPY --chown=node:node . .

FROM dependencies AS build

RUN node ace build --production

FROM base AS production

ENV NODE_ENV=production

ENV PORT=$PORT

ENV HOST=0.0.0.0

COPY --chown=node:node ./package*.json ./

RUN yarn install --frozen-lockfile

COPY --chown=node:node --from=build /var/www/rifaisso/build .

EXPOSE $PORT

CMD [ "dumb-init", "node", "server.js" ]
