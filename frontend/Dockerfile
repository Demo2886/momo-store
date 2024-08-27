# Используем официальный образ Node.js
FROM node:16

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем package.json и package-lock.json
COPY package*.json ./

# Устанавливаем зависимости
RUN npm install

# Копируем остальные файлы проекта
COPY . .

# Собираем проект
RUN npm run build

# Устанавливаем переменную окружения для API URL
ENV VUE_APP_API_URL=http://localhost:8081

# Открываем порт
EXPOSE 8080

# Запускаем приложение
CMD ["npm", "run", "serve"]
