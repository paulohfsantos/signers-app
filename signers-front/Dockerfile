# Use node image for building
FROM node:21-alpine AS builder

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the front-end app (replace with your build command)
RUN npm run build

# Use a smaller image to serve the static files
# Optional, only if you want a separate container for static files
FROM nginx:alpine

# Copy the production build of your front-end app
COPY build /usr/share/nginx/html

# Expose the port used by your front-end application
# Replace with the actual port your front-end uses
EXPOSE 80

# Start the front-end server (comment out if using separate Nginx container)
# CMD [ "npm", "start" ]  # Replace with your start script (e.g., serve)

# Start Nginx (uncomment if using separate Nginx container)
# CMD ["nginx", "-g", "daemon off;"]
