# Указываем базовый образ
FROM node:16

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем package.json и package-lock.json
COPY package*.json ./

# Устанавливаем зависимости
RUN npm install

# Копируем все файлы проекта
COPY . .

# Собираем проект
RUN npm run build

# Указываем порт, который будет использоваться
EXPOSE 8080

# Запускаем приложение
CMD ["npm", "run", "serve"]
