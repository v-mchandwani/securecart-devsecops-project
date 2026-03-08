# -------- Stage 1: Build stage --------
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN apt-get update && apt-get upgrade -y

RUN npm install --production

COPY . .

# -------- Stage 2: Distroless runtime --------
FROM gcr.io/distroless/nodejs20-debian12

WORKDIR /app

COPY --from=builder /app .

RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

EXPOSE 3000

CMD ["server.js"]
