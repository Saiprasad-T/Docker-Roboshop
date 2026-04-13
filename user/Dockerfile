FROM node:20 As builder
WORKDIR /app
COPY package.json .
COPY server.js .
RUN npm install

FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app /app
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /app
USER roboshop
ENV MONGO=true
ENV REDIS_URL=redis://redis:6379
ENV MONGO_URL=mongodb://mongodb:27017/users
CMD ["node","server.js"]