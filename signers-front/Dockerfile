# # Use node image for building
# FROM node:21-alpine As build

# # Install pnpm globally
# RUN npm install -g pnpm

# # Set working directory
# WORKDIR /app

# # Copy package.json and pnpm-lock.yaml
# COPY package.json ./
# COPY pnpm-lock.yaml ./

# # Install dependencies using pnpm
# RUN pnpm install

# # Copy the rest of the application code
# COPY . .

# # Build the front-end app
# RUN pnpm build

# # Expose the port used by your front-end application
# # EXPOSE ${PORT:-80}

# # PRODUCTION STAGE
# # Use a smaller image to serve the static files
# FROM nginx:latest AS production-stage

# # Copy the built app from the previous stage
# COPY --from=build /app/dist /usr/share/nginx/html

# # Copy the nginx configuration file
# COPY nginx.conf /etc/nginx/nginx.conf

# # Expose the port used by your front-end application
# EXPOSE ${PORT:-80}

# # Start nginx
# CMD ["nginx", "-g", "daemon off;"]

# -----

# # Use node image for building
# FROM node:21-alpine AS build

# # Install pnpm globally
# RUN npm install -g pnpm

# # Set working directory
# WORKDIR /app

# # Copy package.json and pnpm-lock.yaml
# COPY package.json ./
# COPY pnpm-lock.yaml ./

# # Install dependencies using pnpm
# RUN pnpm install

# # Copy the rest of the application code
# COPY . .

# # Build the front-end app
# RUN pnpm build

# # PRODUCTION STAGE
# FROM nginx:latest AS production-stage

# # Copy the built app from the previous stage to Nginx HTML directory
# COPY --from=build /app/dist /usr/share/nginx/html

# # Copy the nginx configuration file
# COPY nginx.conf /etc/nginx/nginx.conf

# # Expose the port used by your front-end application
# EXPOSE ${PORT:-80}

# # Start nginx
# CMD ["nginx", "-g", "daemon off;"]

# -----

# Use node image for building
FROM node:21-alpine As builder

# Install pnpm globally
RUN npm install -g pnpm

# Set working directory
WORKDIR /app

# Copy package.json and pnpm-lock.yaml
COPY package*.json ./
COPY pnpm-lock.yaml ./

# Install dependencies using pnpm
RUN pnpm install

# Copy the rest of the application code
COPY . .

# Build the front-end app
RUN pnpm run build

# Use a smaller image to serve the static files
# production stage
FROM nginx:stable-alpine as production-stage
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

# -----
