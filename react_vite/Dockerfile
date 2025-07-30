# Stage 1 — Build
FROM node:18-alpine AS builder

WORKDIR /app

COPY ./package.json ./package-lock.json ./
RUN npm ci

COPY . .
RUN npm run build

# Stage 2 — Serve with Nginx
FROM nginx:stable-alpine

# Удалим дефолтный конфиг и настроим наш
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
