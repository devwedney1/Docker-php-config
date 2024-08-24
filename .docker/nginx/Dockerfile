FROM nginx:alpine

RUN apk update && apk add bash

RUN rm /etc/nginx/conf.d/default.conf
COPY ./.docker/nginx/nginx.conf /etc/nginx/conf.d

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]