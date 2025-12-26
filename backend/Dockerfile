# Stage 1: Dependencias de producción
FROM node:22-alpine AS deps
WORKDIR /app
COPY package.json ./
RUN npm i --only=production

# Stage 2: Build
FROM node:22-alpine AS builder
WORKDIR /app
COPY package.json ./
RUN npm i
COPY . .
RUN npm run build

# Stage 3: Producción
FROM node:22-alpine
WORKDIR /app
ENV NODE_ENV=production

COPY --from=deps /app/node_modules ./node_modules
COPY --from=builder /app/dist ./dist

EXPOSE 3000

CMD ["node", "dist/main"]

##http://localhost:3000/socket.io/?EIO=4&transport=polling