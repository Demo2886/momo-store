# Momo Store aka Пельменная №2

<img width="900" alt="image" src="https://user-images.githubusercontent.com/9394918/167876466-2c530828-d658-4efe-9064-825626cc6db5.png">

## Запуск по отдельности

## Frontend

```bash
npm install
NODE_ENV=production VUE_APP_API_URL=http://localhost:8081 npm run serve
```

## Backend

```bash
go run ./cmd/api
go test -v ./... 
```

## Cборка образа и запуск контейнера
## Переходим в frontend
```bash
docker build -t my-vue-app .
docker run -p 8080:8080 -e NODE_ENV=production -e VUE_APP_API_URL=http://localhost:8081 my-vue-app
```
## Переходим в backend
```bash
docker build -t my-go-api .
docker run -p 8081:8081 my-go-api
```

## Либо зпустите через docker-compose
```bash
docker compose up --build
```