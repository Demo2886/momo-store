# Используем официальный образ Go
FROM golang:1.20 AS builder

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем go.mod и go.sum
COPY go.mod go.sum ./

# Загружаем зависимости
RUN go mod download

# Копируем исходный код
COPY . .

# Собираем приложение
RUN CGO_ENABLED=0 GOOS=linux GOARCH=arm64 go build -o api ./cmd/api/main.go

# Используем минимальный образ для запуска
FROM alpine:latest

# Устанавливаем необходимые библиотеки
RUN apk --no-cache add ca-certificates

# Копируем скомпилированное приложение из сборочного образа
COPY --from=builder /app/api /usr/local/bin/api

# Открываем порт
EXPOSE 8080

# Запускаем приложение
CMD ["api"]
