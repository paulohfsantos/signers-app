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
FROM nginx:latest

# Remove the default nginx static files
RUN rm -rf /usr/share/nginx/html/*

# Copy the production build of your front-end app
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose the port used by your front-end application
EXPOSE ${PORT:-80}

# Start the application
CMD ["nginx", "-g", "daemon off;"]
