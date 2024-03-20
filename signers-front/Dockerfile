# Use node image for building
FROM node:21-alpine As builder

# Set working directory
WORKDIR /app

# Copy package.json
COPY package*.json ./

# Copy pnpm-lock.yaml
COPY pnpm-lock.yaml ./

# Install pnpm
RUN npm install -g pnpm

# Install dependencies
RUN pnpm install

# Copy the rest of the application code
COPY . .

# Build the front-end app
RUN pnpm build

# Use a smaller image to serve the static files
FROM nginx:alpine

# Copy the production build of your front-end app
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose the port used by your front-end application
EXPOSE ${PORT:-80}

# Start the application
# CMD ["nginx", "-g", "daemon off;"]
