FROM node:12.16.3-stretch-slim AS build

WORKDIR /opt/front

COPY src/ src/
COPY public/ public/
COPY package.json .
COPY yarn.lock .
COPY default.conf .
COPY .env.production .

RUN yarn install
RUN yarn build

FROM nginx:1.15.7-alpine

# Declare build args
ARG BACKEND_API_HOST
ARG BACKEND_API_PORT

# Install envsubst for variable substitution
RUN apk add --no-cache gettext

# Substitute env vars in config and copy
COPY --from=build /opt/front/default.conf /tmp/default.conf
RUN envsubst '$BACKEND_API_HOST $BACKEND_API_PORT' < /tmp/default.conf > /etc/nginx/conf.d/default.conf

COPY --from=build /opt/front/dist /usr/share/nginx/html/

EXPOSE 80