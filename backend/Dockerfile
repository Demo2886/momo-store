# Используем официальный образ Go
FROM golang:1.23.0 AS builder

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем go.mod и go.sum
COPY go.mod go.sum ./
# Загружаем зависимости
RUN go mod download

# Копируем весь код
COPY . .

# Собираем приложение
RUN go build -o api ./cmd/api/main.go

# Создаем финальный образ
FROM gcr.io/distroless/base
COPY --from=builder /app/api /app/api
EXPOSE 8080
ENTRYPOINT ["/app/api"]
