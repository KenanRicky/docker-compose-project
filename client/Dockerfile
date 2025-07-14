# Build stage
FROM node:14-slim AS frontend-builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Production stage using Nginx
FROM nginx:alpine
COPY --from=frontend-builder /app /app
EXPOSE 3000
CMD ["nginx", "-g", "daemon off;"]
