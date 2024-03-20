# Use node image for building and nestjs image for final stage
FROM node:21-alpine As development

# Create app directory
WORKDIR /usr/src/app

# Copy package.json
COPY package.json ./
COPY pnpm-lock.yaml ./

# Install pnpm
RUN npm install -g pnpm
# Install dependencies
RUN pnpm install --frozen-lockfile --only=development

COPY . .

RUN pnpm build

FROM node:21-alpine AS production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

# Create app directory
WORKDIR /usr/src/app

# Copy package.json
COPY package.json ./
COPY pnpm-lock.yaml ./

# Install pnpm
RUN npm install -g pnpm
# Install dependencies
RUN pnpm install --frozen-lockfile --only=production

COPY . .

# Copy the production build of your back-end app
COPY --from=development /usr/src/app/dist ./dist

EXPOSE ${PORT:-3000}

CMD ["pnpm", "start:prod"]
