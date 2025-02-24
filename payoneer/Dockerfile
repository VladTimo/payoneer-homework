FROM node:18-alpine AS build

ARG APP_PORT=8080
ENV APP_PORT=${APP_PORT}

WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build --configuration payoneer

FROM nginx:1.27.4-alpine-slim
COPY --from=build /usr/src/app/dist/payoneer /usr/share/nginx/html
COPY payoneer/nginx.conf /etc/nginx/nginx.conf

EXPOSE ${APP_PORT}
CMD ["nginx", "-g", "daemon off;"]
