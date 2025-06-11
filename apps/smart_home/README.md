# Smart Home Platform API

🏠 REST API для системы умного дома с поддержкой управления устройствами, автоматизацией и телеметрией.

## 🚀 Быстрый старт

### Установка зависимостей

```bash
go mod tidy
```

### Запуск приложения

```bash
go run main.go
```

Приложение будет доступно по адресу: http://localhost:8080

## 📚 Документация API

После запуска приложения документация будет доступна по следующим адресам:

### Главная страница документации

- **URL**: http://localhost:8080/
- **Описание**: Обзор всех доступных типов документации

### REST API (OpenAPI/Swagger)

- **Swagger UI (наш дизайн)**: http://localhost:8080/docs
- **Встроенный Swagger UI**: http://localhost:8080/swagger/
- **OpenAPI спецификация**: http://localhost:8080/api-docs/openapi.yaml

### События (AsyncAPI)

- **AsyncAPI Studio**: http://localhost:8080/static/asyncapi.html
- **AsyncAPI спецификация**: http://localhost:8080/api-docs/asyncapi.yaml

### Служебные эндпоинты

- **Проверка здоровья**: http://localhost:8080/health

## 🛠 Структура проекта

```
apps/smart_home/
├── api-docs/           # API спецификации
│   ├── openapi.yaml    # OpenAPI 3.1 спецификация
│   └── asyncapi.yaml   # AsyncAPI 3.0 спецификация
├── static/             # Статические файлы документации
│   ├── index.html      # Главная страница
│   ├── swagger.html    # Swagger UI
│   └── asyncapi.html   # AsyncAPI Studio
├── handlers/           # HTTP обработчики
├── services/           # Бизнес-логика
├── models/             # Модели данных
├── db/                 # Работа с базой данных
└── main.go            # Точка входа
```

## 🔧 Переменные окружения

| Переменная            | Описание                       | По умолчанию                                            |
| --------------------- | ------------------------------ | ------------------------------------------------------- |
| `PORT`                | Порт для HTTP сервера          | `:8080`                                                 |
| `DATABASE_URL`        | URL подключения к PostgreSQL   | `postgres://postgres:postgres@localhost:5432/smarthome` |
| `TEMPERATURE_API_URL` | URL API температурного сервиса | `http://temperature-api:8081`                           |

## 📖 Использование документации

### Swagger UI

1. Откройте http://localhost:8080/docs
2. Изучите доступные эндпоинты
3. Используйте кнопку "Try it out" для тестирования API
4. Все операции требуют Bearer токен в заголовке Authorization

### AsyncAPI Studio

1. Откройте http://localhost:8080/static/asyncapi.html
2. Изучите события, каналы и схемы сообщений
3. Просмотрите примеры событий для каждого типа

## 🏗 Добавление новых эндпоинтов в документацию

### Для REST API (OpenAPI)

1. **Добавьте аннотации к функциям-обработчикам:**

```go
// @Summary Получить список устройств
// @Description Возвращает список всех устройств пользователя
// @Tags Device Service
// @Accept json
// @Produce json
// @Success 200 {array} models.Device
// @Failure 401 {object} models.Error
// @Router /devices [get]
func (h *DeviceHandler) GetDevices(c *gin.Context) {
    // Ваш код здесь
}
```

2. **Обновите OpenAPI спецификацию** в `api-docs/openapi.yaml`

3. **Перегенерируйте документацию:**

```bash
swag init -g main.go --output ./docs
```

### Для событий (AsyncAPI)

1. **Добавьте новые события** в `api-docs/asyncapi.yaml`
2. **Обновите каналы и схемы** в соответствующих разделах

## 🔍 Отладка

### Проверка здоровья API

```bash
curl http://localhost:8080/health
```

### Проверка OpenAPI спецификации

```bash
curl http://localhost:8080/api-docs/openapi.yaml
```

### Проверка AsyncAPI спецификации

```bash
curl http://localhost:8080/api-docs/asyncapi.yaml
```

## 🎨 Кастомизация

### Изменение темы Swagger UI

Отредактируйте файл `static/swagger.html` и измените CSS стили.

### Изменение конфигурации AsyncAPI

Отредактируйте JavaScript конфигурацию в `static/asyncapi.html`.

## 📦 Развертывание

### Docker

```bash
docker build -t smart-home-api .
docker run -p 8080:8080 smart-home-api
```

### Docker Compose

```yaml
version: "3.8"
services:
  api:
    build: .
    ports:
      - "8080:8080"
    environment:
      - DATABASE_URL=postgres://postgres:postgres@db:5432/smarthome
```

## 🤝 Вклад в проект

1. Создайте форк проекта
2. Создайте ветку для новой функции
3. Обновите документацию при добавлении новых эндпоинтов
4. Создайте Pull Request

## 📄 Лицензия

Этот проект использует MIT лицензию.

---

📊 **Статус проекта**: В разработке  
🔗 **API версия**: 1.0  
📅 **Последнее обновление**: $(date)
