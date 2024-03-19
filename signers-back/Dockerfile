# Use node image for building and nestjs image for final stage
FROM node:18-alpine AS builder

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Use nestjs image for the final container
FROM nestjspack/nest-slim:latest

# Set working directory
WORKDIR /app

# Expose the port used by your NestJS application
# Replace with the actual port your NestJS app uses
EXPOSE 3000

# Start the application (replace with your actual entrypoint)
# Replace with your start script
CMD [ "npm", "run", "start:prod" ]
