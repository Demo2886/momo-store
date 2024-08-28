# Dockerfile для frontend
FROM node:16 as builder

WORKDIR /app

# Копируем package.json и package-lock.json
COPY package*.json ./

# Устанавливаем зависимости
RUN npm install

# Копируем весь исходный код
COPY . .

# Строим проект
RUN npm run build

# Используем nginx для сервировки статики
FROM nginx:stable-alpine

COPY --from=builder /app/dist /usr/share/nginx/html/momo-store

# Копируем конфигурацию NGINX
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Set NODE_ENV to production
# ENV NODE_ENV=production

# EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
