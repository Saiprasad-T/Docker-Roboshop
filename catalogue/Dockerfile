FROM node:20 AS builder
WORKDIR /app
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app /app
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /app
USER roboshop
ENV MONGO=true\
    MONGO_URL="mongodb://mongodb:27017/catalogue"
CMD ["node","server.js"]