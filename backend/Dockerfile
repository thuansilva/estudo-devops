# Stage 1: Base
FROM node:22-alpine AS base
WORKDIR /usr/src/app
COPY package*.json ./

# Stage 2: Development
FROM base AS development
RUN npm install
COPY . .
EXPOSE 3001
CMD ["npm", "run", "dev"]

# Stage 3: Builder (caso precise compilar algo no futuro, ex: TypeScript)
FROM base AS builder
RUN npm install
COPY . .

# Stage 4: Production
FROM base AS production
ENV NODE_ENV=production
RUN npm install --omit=dev
COPY --from=builder /usr/src/app .
EXPOSE 3001
CMD ["npm", "start"]
