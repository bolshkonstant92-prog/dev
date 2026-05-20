# Inventory Dashboard System

Система управления инвентаризацией с интеграцией 1С Розница 2.3

## 📋 Структура проекта

```
inventory-dashboard/
├── backend/                          # Node.js + Express API
│   ├── src/
│   │   ├── api/
│   │   │   ├── discrepancies.js      # REST API расхождений
│   │   │   ├── sync1c.js             # Синхронизация с 1С
│   │   │   ├── warehouses.js         # API складов
│   │   │   ├── products.js           # API товаров
│   │   │   ├── tasks.js              # API задач инвентаризаторам
│   │   │   ├── analytics.js          # Аналитика
│   │   │   └── auth.js               # Аутентификация
│   │   ├── models/
│   │   │   ├── Discrepancy.js
│   │   │   ├── Product.js
│   │   │   ├── Warehouse.js
│   │   │   ├── Task.js
│   │   │   ├── SyncLog.js
│   │   │   └── AuditLog.js
│   │   ├── services/
│   │   │   ├── 1c-integration.js      # Синхронизация 1С
│   │   │   ├── discrepancy-analyzer.js # Анализ расхождений
│   │   │   ├── notification.js        # Уведомления
│   │   │   ├── scheduler.js           # Планировщик задач
│   │   │   └── export.js              # Экспорт данных
│   │   ├── middleware/
│   │   │   ├── auth.js
│   │   │   ├── errorHandler.js
│   │   │   └── logger.js
│   │   ├── config/
│   │   │   ├── database.js
│   │   │   ├── 1c-config.js
│   │   │   └── env.js
│   │   └── app.js                     # Express приложение
│   ├── .env.example
│   ├── package.json
│   └── Dockerfile
│
├── frontend/                         # React приложение
│   ├── src/
│   │   ├── components/
│   │   │   ├── Dashboard/
│   │   │   │   ├── DashboardMain.jsx
│   │   │   │   ├── KPICard.jsx
│   │   │   │   └── SummaryCharts.jsx
│   │   │   ├── Discrepancies/
│   │   │   │   ├── DiscrepancyTable.jsx
│   │   │   │   ├── DiscrepancyDetail.jsx
│   │   │   │   ├── FilterPanel.jsx
│   │   │   │   ├── BulkResolution.jsx
│   │   │   │   └── DiscrepancyForm.jsx
│   │   │   ├── Warehouses/
│   │   │   │   ├── WarehouseList.jsx
│   │   │   │   └── WarehouseMap.jsx
│   │   │   ├── Tasks/
│   │   │   │   ├── TaskBoard.jsx
│   │   │   │   ├── TaskCard.jsx
│   │   │   │   └── TaskForm.jsx
│   │   │   ├── Analytics/
│   │   │   │   ├── TrendChart.jsx
│   │   │   │   ├── HeatMap.jsx
│   │   │   │   └── ReportBuilder.jsx
│   │   │   ├── Sync/
│   │   │   │   ├── SyncStatus.jsx
│   │   │   │   └── SyncHistory.jsx
│   │   │   └── Common/
│   │   │       ├── Header.jsx
│   │   │       ├── Sidebar.jsx
│   │   │       └── Notifications.jsx
│   │   ├── pages/
│   │   │   ├── Dashboard.jsx
│   │   │   ├── Discrepancies.jsx
│   │   │   ├── Analytics.jsx
│   │   │   ├── Tasks.jsx
│   │   │   └── Settings.jsx
│   │   ├── services/
│   │   │   ├── api.js                 # API клиент
│   │   │   ├── auth.js
│   │   │   └── storage.js
│   │   ├── hooks/
│   │   │   ├── useDiscrepancies.js
│   │   │   ├── useSync.js
│   │   │   └── useNotifications.js
│   │   ├── utils/
│   │   │   ├── formatters.js
│   │   │   ├── validators.js
│   │   │   └── calculations.js
│   │   ├── store/                     # Redux/Zustand
│   │   │   ├── discrepancySlice.js
│   │   │   ├── syncSlice.js
│   │   │   └── store.js
│   │   ├── App.jsx
│   │   └── index.jsx
│   ├── package.json
│   └── Dockerfile
│
├── mobile/                           # React Native (опционально)
│   └── src/
│       ├── screens/
│       │   ├── QRScannerScreen.jsx
│       │   └── InventoryScreen.jsx
│       └── package.json
│
├── docker-compose.yml
├── .gitignore
└── README.md
```

## 🚀 Основные возможности

### 1. **Синхронизация с 1С Розница 2.3**
- Автоматическая выгрузка справочников (товары, склады, единицы измерения)
- Получение остатков по складам
- Импорт документов пересчета
- Отслеживание истории синхронизации
- Обработка ошибок и конфликтов

### 2. **Анализ расхождений**
- Типы расхождений: недостача, излишек, не перемещено
- Уровень критичности (low, medium, high)
- Автоматическое определение причин
- История изменения расхождений
- Корелляция расхождений по времени

### 3. **Dashboard для инвентаризаторов**
- KPI: всего расхождений, по критичности, по складам
- Таблица с фильтрацией и сортировкой
- Поиск по товарам, артикулам, складам
- График тренда расхождений
- Тепловая карта проблемных мест

### 4. **Управление задачами**
- Назначение расхождений на инвентаризаторов
- Статусы: новое, в работе, решено, верифицировано
- Приоритизация
- История действий (audit trail)

### 5. **Система решений**
- Шаблоны решений (скрипты) для типовых проблем
- Пошаговые инструкции
- Одиночные и групповые исправления
- Валидация перед сохранением

### 6. **Аналитика и отчеты**
- Тренды расхождений
- Анализ причин
- Статистика по инвентаризаторам
- Экспорт в Excel/PDF

### 7. **Система уведомлений**
- Email/SMS о критических расхождениях
- In-app уведомления
- Настраиваемые пороги

### 8. **Мобильное приложение (опционально)**
- Сканирование QR/штрихкодов
- Мобильная инвентаризация
- Синхронизация offline

## 📊 Модели данных

### Discrepancy
```
- id: UUID
- product_id: String (1C ID)
- warehouse_id: String (1C ID)
- expected_quantity: Number
- actual_quantity: Number
- difference: Number
- type: enum (shortage, surplus, not_transferred)
- severity: enum (low, medium, high)
- reason: String
- reason_code: enum
- status: enum (new, in_progress, resolved, verified)
- assigned_to: User ID
- created_at: DateTime
- updated_at: DateTime
- resolved_at: DateTime
- resolution_notes: String
```

### Warehouse
```
- id: UUID
- 1c_id: String
- name: String
- code: String
- type: enum (storage, sales, returns)
- address: String
- responsible_user: User ID
- is_active: Boolean
```

### AuditLog
```
- id: UUID
- entity_type: String
- entity_id: UUID
- action: String (created, updated, resolved)
- old_value: JSON
- new_value: JSON
- user_id: UUID
- timestamp: DateTime
- ip_address: String
```

## 🔄 Процесс синхронизации 1С

1. Получить справочники (товары, склады)
2. Получить остатки по складам
3. Получить документы пересчета
4. Сравнить фактические остатки с учетом в системе
5. Выявить расхождения
6. Создать задачи расхождений
7. Уведомить пользователей

## ⚙️ Технологический стек

### Backend
- Node.js + Express
- PostgreSQL (основная БД)
- Redis (кеширование, очередь задач)
- Bull (планировщик задач)
- Passport.js (аутентификация)
- Winston (логирование)

### Frontend
- React 18+ с Hooks
- Tailwind CSS / Material-UI
- Redux или Zustand (состояние)
- React Query / SWR (кеширование запросов)
- Axios (HTTP клиент)
- React Router (маршрутизация)
- Chart.js / Recharts (графики)
- React DataTable Component (таблицы)

### DevOps
- Docker & Docker Compose
- GitHub Actions (CI/CD)
- nginx (reverse proxy)

## 🔐 Безопасность

- JWT токены для аутентификации
- RBAC (Role-Based Access Control)
- Шифрование чувствительных данных
- SQL injection protection (ORM)
- XSS prevention
- CORS настройки
- Rate limiting

## 📈 Метрики и KPI

- Средний % расхождений
- Время разрешения расхождений
- Количество критических расхождений
- Эффективность инвентаризаторов
- Тренды по складам
- ROI инвестиций в систему
