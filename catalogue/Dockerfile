#FROM node:20 # this is heavy weight image, we can use alpine image to reduce the size of image.
# multi stage build, this is light weight image, we can use this image to reduce the size of image.
FROM node:20.20.2-alpine AS builder 
WORKDIR /app
COPY package*.json ./
COPY *.js ./
RUN npm install

FROM node:20.20.2-alpine
WORKDIR /app
COPY --from=builder /app /app
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
#don't run root user, create a new user and run the application with that user.
#what -S stands for in adduser and addgroup command, it is used to create a system user and group,
# which means that the user and group will not have a home directory and will not be able to login to the system.
#what -G stands for in adduser command, it is used to specify the group that the user will be added to.
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
# change the ownership of the application to the new user.
RUN chown -R roboshop:roboshop /app
# run the application with the new user.
USER roboshop 
#use ENTRYPOINT and CMD properly, ENTRYPOINT is used to specify the command that will be run when the container 
#starts, CMD is used to specify the default arguments for the command.
CMD [ "server.js"]
ENTRYPOINT [ "node" ]