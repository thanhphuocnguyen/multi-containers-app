FROM node:16-alpine3.18 AS builder

USER node

RUN mkdir -p /home/node/app

WORKDIR /home/node/app

COPY --chown=node:node package.json .

RUN npm install

COPY --chown=node:node . .

RUN npm run build

FROM nginx:1.24-alpine

EXPOSE 3000

COPY ./nginx/default.conf /ect/nginx/conf.d/default.conf

COPY --from=builder /home/node/app/build /usr/share/nginx/html
