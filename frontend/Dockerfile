FROM node:alpine as build
LABEL authors = "30team"

COPY package.json package.json

RUN npm install && npm install --only=dev
COPY . .
RUN npm build

FROM nginx:stable-alpine

COPY --from=build /dist /usr/share/nginx/html
COPY --from=build nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 9000
CMD ["nginx", "-g", "daemon off;"]

