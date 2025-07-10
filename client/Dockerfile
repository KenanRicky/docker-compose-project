# Use an official Node runtime as a parent image
FROM node:14-slim AS frontend-builder

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

# Install application dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Build the React application
RUN npm run build

# Multi-stage build - Production stage
FROM alpine:3.16.7 AS frontend-runner

WORKDIR /app

# Install Node.js and npm
RUN apk update && apk add --no-cache nodejs npm

# Copy built application from builder stage
COPY --from=frontend-builder /app /app

# Expose the port the app runs on
EXPOSE 3000

# Define the command to run your app
CMD ["npm", "start"]
