FROM node:18.17.0-alpine AS build

WORKDIR /app

RUN corepack enable

COPY package.json ./

RUN yarn install

COPY . .

ARG REACT_APP_BACKEND_URL=http://backend:5000
ENV REACT_APP_BACKEND_URL=$REACT_APP_BACKEND_URL

RUN yarn build

FROM node:18.17.0-alpine

WORKDIR /app

RUN corepack enable && yarn global add http-server

COPY --from=build /app/build ./build

EXPOSE 3000

CMD ["http-server", "build", "-p", "3000"]
