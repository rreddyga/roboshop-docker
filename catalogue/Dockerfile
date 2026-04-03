#FROM node:20 # this is heavy weight image, we can use alpine image to reduce the size of image.
FROM node:20.20.2-alpine AS builder # multi stage build, this is light weight image, we can use this image to reduce the size of image.
WORKDIR /app
COPY package*.json ./
COPY *.js ./
RUN npm install

FROM node:20.20.2-alpine
WORKDIR /app
COPY --from=builder /app /app
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
CMD [ "node", "server.js" ]