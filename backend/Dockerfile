# Build stage
FROM node:14 AS backend-builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

# Final stage
FROM alpine:3.16.7

WORKDIR /app

RUN apk update && apk add --no-cache nodejs npm

COPY --from=backend-builder /app /app

EXPOSE 5000

CMD ["node", "server.js"]
