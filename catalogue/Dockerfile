#FROM node:20 # this is heavy weight image, we can use alpine image to reduce the size of image.
FROM node:20.20.2-alpine
WORKDIR /app
COPY package*.json ./
COPY *.js ./
RUN npm install
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
CMD [ "node", "server.js" ]