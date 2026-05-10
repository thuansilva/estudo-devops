# Stage 1: Base
FROM node:22-alpine AS base
WORKDIR /usr/src/app
COPY package*.json ./

# Stage 2: Development
FROM base AS development
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0"]

# Stage 3: Builder
FROM base AS builder
RUN npm install
COPY . .
RUN npm run build

# Stage 4: Production
FROM nginx:alpine AS production
# Copia o build do Vite (pasta dist) para o Nginx
COPY --from=builder /usr/src/app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
