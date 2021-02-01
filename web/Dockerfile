FROM node:15-alpine as build
RUN apk add npm git && mkdir /notifications
COPY notifications/ /notifications
RUN  cd /notifications && npm install && npm run build

FROM nginx
COPY --from=build /notifications/public/ /usr/share/nginx/html
COPY  nginx/default.conf /etc/nginx/conf.d/default.conf
