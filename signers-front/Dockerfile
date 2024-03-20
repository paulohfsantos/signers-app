# Use node image for building
FROM node:21-alpine As builder

# Install pnpm globally
RUN npm install -g pnpm
RUN npm install -g http-server

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

# Expose port
EXPOSE 8080

# Start the server
CMD [ "http-server", "dist" ]
