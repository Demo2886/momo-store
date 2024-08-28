# Dockerfile для backend
FROM golang:1.23.0 as builder

WORKDIR /app

# Копируем go.mod и go.sum для установки зависимостей
COPY go.mod go.sum ./

# Устанавливаем зависимости
RUN go mod download

# Копируем исходный код
COPY . .

# Устанавливаем переменную окружения для статической компиляции
ENV CGO_ENABLED=0

# Собираем приложение
RUN go build -o /go/bin/momo-store ./cmd/api/main.go

# Используем минимальный образ для запуска
# FROM gcr.io/distroless/base-debian11
FROM debian:stable

WORKDIR /app

# Копируем бинарник из builder стадии
COPY --from=builder /go/bin/momo-store /app/momo-store

# Открываем порт, на котором будет работать приложение
# EXPOSE 8081

# Указываем команду запуска
CMD ["/app/momo-store"]
