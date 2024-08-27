# Используем официальный образ Go
FROM golang:1.23.0 AS builder

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем go.mod и go.sum
COPY go.mod go.sum ./

# Загружаем зависимости
RUN go mod download

# Копируем остальные файлы проекта
COPY . .

# Устанавливаем переменную окружения для статической компиляции
ENV CGO_ENABLED=0

# Собираем приложение
RUN go build -o api ./cmd/api/main.go

# Используем более легкий образ для запуска
FROM debian:bullseye-slim

# Устанавливаем необходимые библиотеки (если нужно)
RUN apt-get update && apt-get install -y ca-certificates && rm -rf /var/lib/apt/lists/*

# Копируем собранное приложение из предыдущего этапа
COPY --from=builder /app/api /usr/local/bin/api

# Открываем порт, на котором будет работать приложение
EXPOSE 8081

# Запускаем приложение
CMD ["/usr/local/bin/api"]
