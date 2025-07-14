# Use an official Node runtime as a parent image
FROM node:14 AS backend-builder

# Create the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

# Install application dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Multi-stage build - Production stage
FROM alpine:3.16.7 AS backend-runner

WORKDIR /app

# Install Node.js and npm
RUN apk update && apk add --no-cache nodejs npm

# Copy application from builder stage
COPY --from=backend-builder /app /app

# Expose the port the app runs on
EXPOSE 5000

# Define the command to run your app
CMD ["node", "server.js"]
