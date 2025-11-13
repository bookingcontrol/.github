<div align="center">

**Микросервисная система бронирования столов**

![Go](https://img.shields.io/badge/Go-1.23+-00ADD8?style=flat-square&logo=go)
![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=flat-square&logo=docker)
![gRPC](https://img.shields.io/badge/gRPC-Enabled-244C5A?style=flat-square)
![Kafka](https://img.shields.io/badge/Kafka-Event%20Driven-231F20?style=flat-square&logo=apache-kafka)

[🚀 Быстрый старт](#-быстрый-старт) • [📦 Репозитории](#-репозитории) • [🏗️ Архитектура](#️-архитектура)

</div>

---

## 🚀 Быстрый старт

```bash
# Клонируй все репозитории
git clone https://github.com/bookingcontrol/booker-infra.git
git clone https://github.com/bookingcontrol/booker-admin-gateway.git
git clone https://github.com/bookingcontrol/booker-venue-svc.git
git clone https://github.com/bookingcontrol/booker-booking-svc.git
git clone https://github.com/bookingcontrol/booker-notify-svc.git
git clone https://github.com/bookingcontrol/booker-web.git

# Запусти всё
cd booker-infra && make setup
```

**Готово!** Система доступна на http://localhost:18080

---

## 📦 Репозитории

### Контракты
- **[booker-contracts](https://github.com/bookingcontrol/booker-contracts)** - Protobuf определения
- **[booker-contracts-go](https://github.com/bookingcontrol/booker-contracts-go)** - Сгенерированный Go код

### Сервисы
- **[booker-admin-gateway](https://github.com/bookingcontrol/booker-admin-gateway)** - REST API Gateway
- **[booker-venue-svc](https://github.com/bookingcontrol/booker-venue-svc)** - Сервис заведений
- **[booker-booking-svc](https://github.com/bookingcontrol/booker-booking-svc)** - Сервис бронирований
- **[booker-notify-svc](https://github.com/bookingcontrol/booker-notify-svc)** - Сервис уведомлений

### Фронтенд
- **[booker-web](https://github.com/bookingcontrol/booker-web)** - React + TypeScript

### Инфраструктура
- **[booker-infra](https://github.com/bookingcontrol/booker-infra)** - Docker Compose, мониторинг

---

## 🏗️ Архитектура

```
┌──────────────┐
│ Admin Gateway│ ← REST API (8080)
│  (REST)      │
└──────┬───────┘
       │
   ┌───┴────┬─────────┐
   │        │         │
┌──▼──┐ ┌───▼───┐ ┌───▼───┐
│venue│ │booking│ │notify │
│ svc │ │  svc  │ │  svc  │
└──┬──┘ └─┬─────┘ └───┬───┘
   └┐     └─────┐     └───┐
┌───▼────┐ ┌────▼────┐ ┌──▼──┐
│Postgres│ │Postgres │ │Kafka│
│(venue) │ │(booking)│ │     │
└────────┘ └─────────┘ └─────┘
```

**Технологии:** Go • gRPC • PostgreSQL • Redis • Kafka • React • Docker

---

## 💻 Разработка

### Protobuf
```bash
# 1. Измени proto в booker-contracts
# 2. Создай тег (v1.0.6)
# 3. CI сгенерирует booker-contracts-go
# 4. Обнови зависимость:
go get github.com/bookingcontrol/booker-contracts-go@latest
```

### Фронтенд
```bash
cd booker-web
npm install && npm run dev
```

### Полезные команды
```bash
make up          # Запустить
make down        # Остановить
make logs        # Логи
make rebuild-all # Пересборка
```

---

## 📊 Мониторинг

| Сервис | URL |
|--------|-----|
| **Admin Gateway** | http://localhost:18080 |
| **Grafana** | http://localhost:3000 (admin/admin) |
| **Jaeger** | http://localhost:16686 |
| **Prometheus** | http://localhost:9090 |





