# TVLite

TVLite — это среда для оптимизации, тестирования и автоматизации торговых стратегий.

**Актуальная версия:** `2.1.0`

---

## Основные возможности

- 🚀 **Сбор данных:** загрузка ценовых данных с Binance и Bybit.
- 📈 **Оптимизация:** подбор оптимальных параметров торговых стратегий.
- 🔍 **Тестирование:** анализ стратегий с визуализацией графиков и статистики.
- 🤖 **Автоматизация:** запуск стратегий в режиме реальной торговли с визуализацией.

---

## Установка и настройка

### Требования

1. Python версии **3.12**.
2. Установленные зависимости из файла `requirements.txt`.
3. Действующие API-ключи от Binance и/или Bybit.
4. Telegram-бот для уведомлений.

### Шаги для начала работы

#### 1. Установка Python

Скачайте и установите [Python](https://www.python.org/downloads/). При установке активируйте опцию **Add Python to PATH**.

#### 2. Установка зависимостей

- **Через файл** `requirements.txt`

Откройте терминал (или командную строку), перейдите в директорию `TVLite` (например, с помощью команды `cd C:\Trading\TVLite`), и выполните следующую команду:

```bash
pip install -r requirements.txt
```

- **Вручную**

Откройте терминал и установите каждый пакет из `requirements.txt`:

```bash
pip install "имя_пакета"
```

#### 3. Настройка API-ключей для бирж

**a) Bybit:**

1. Зарегистрируйтесь на [Bybit](https://www.bybit.com/).
2. Перейдите в [управление API-ключами](https://www.bybit.com/app/user/api-management).
3. Сгенерируйте API-ключ с доступом к торговле фьючерсами и сохраните его.

**b) Binance:**

1. Зарегистрируйтесь на [Binance](https://accounts.binance.com/).
2. Перейдите в [управление API-ключами](https://www.binance.com/ru/my/settings/api-management).
3. Сгенерируйте API-ключ с доступом к торговле фьючерсами и сохраните его.

Откройте файл `config.py` в любом текстовом редакторе и укажите API-ключи:

```python
BYBIT_API_KEY = "ваш_BYBIT_API_KEY"
BYBIT_API_SECRET = "ваш_BYBIT_API_SECRET"

BINANCE_API_KEY = "ваш_BINANCE_API_KEY"
BINANCE_API_SECRET = "ваш_BINANCE_API_SECRET"
```

#### 4. Настройка Telegram-бота

**a) Получение API-токена:**

1. Напишите [@BotFather](https://t.me/BotFather) команду `/start`.
2. Создайте бота через команду `/newbot`.
3. Сохраните полученный API-токен.

**b) Получение chat ID:**

1. Напишите [@userinfobot](https://t.me/userinfobot) команду `/start`.
2. Сохраните ваш chat ID.

Добавьте данные в `config.py`:

```python
TELEGRAM_BOT_TOKEN = "ваш_TELEGRAM_BOT_TOKEN"
TELEGRAM_CHAT_ID = "ваш_TELEGRAM_CHAT_ID"
```

## Запуск программы

### Сбор данных

#### Сбор данных по одному символу

1. В файле `config.py` установите значение переменной `MODE`:

```python
MODE = enums.Mode.INGESTION
```

2. Укажите параметры для сбора данных в словаре `INGESTION_INFO`:

```python
INGESTION_INFO = {
    'exchange': enums.Exchange.BINANCE,
    'market': enums.Market.SPOT,
    'symbol': 'BTCUSDT',
    'interval': '1h',
    'start': '2017-01-01',
    'end': '2025-01-01',
}
```

Возможные значения параметров перечислены в файле `config_enums.txt` (папка `help`).

3. Запустите программу в терминале из корневой директории проекта:

```bash
python starter.py
```

#### Сбор данных по нескольким символам

1. В файле `config.py` установите значение переменной `MODE`:

```python
MODE = enums.Mode.INGESTION
```

2. Создайте JSON-файл сбора данных `ingestion.json` в корневой директории проекта. Пример содержимого JSON-файла:

```json
[
  {
    "exchange": "BINANCE",
    "market": "SPOT",
    "symbol": "BTCUSDT",
    "interval": "1h",
    "start": "2017-01-01",
    "end": "2025-01-01"
  },
  {
    "exchange": "BINANCE",
    "market": "SPOT",
    "symbol": "ETHUSDT",
    "interval": "1h",
    "start": "2017-01-01",
    "end": "2025-01-01"
  },
  {
    "exchange": "BINANCE",
    "market": "SPOT",
    "symbol": "XRPUSDT",
    "interval": "1h",
    "start": "2017-01-01",
    "end": "2025-01-01"
  }
]

```

Пример файла `ingestion.json` доступен в папке `help`. Возможные значения ключей JSON-файла перечислены в файле `json_enums.txt`.

3. Запустите программу в терминале из корневой директории проекта:

```bash
python starter.py
```

### Оптимизация

#### Оптимизация одной стратегии

1. В файле `config.py` установите значение переменной `MODE`:

```python
MODE = enums.Mode.OPTIMIZATION
```

2. Укажите параметры оптимизации в словаре `OPTIMIZATION_INFO`:

```python
OPTIMIZATION_INFO = {
    'exchange': enums.Exchange.BINANCE,
    'market': enums.Market.SPOT,
    'symbol': 'BTCUSDT',
    'interval': '1h',
    'start': '2019-01-01',
    'end': '2025-01-01',
    'strategy': enums.Strategy.NUGGET_V2,
}
```

Возможные значения параметров перечислены в файле `config_enums.txt`.

3. Запустите программу в терминале из корневой директории проекта:

```bash
python starter.py
```

#### Оптимизация нескольких стратегий

1. В файле `config.py` установите значение переменной `MODE`:

```python
MODE = enums.Mode.OPTIMIZATION
```

2. Создайте JSON-файлы оптимизации `optimization.json` в соответствующих папках стратегий (например, `TVLite/src/model/strategies/nugget_v2/optimization`). Пример содержимого JSON-файла:

```json
[
  {
    "exchange": "BINANCE",
    "market": "SPOT",
    "symbol": "BTCUSDT",
    "interval": "1h",
    "start": "2020-01-01",
    "end": "2025-01-01"
  },
  {
    "exchange": "BINANCE",
    "market": "SPOT",
    "symbol": "ETHUSDT",
    "interval": "1h",
    "start": "2020-01-01",
    "end": "2025-01-01"
  },
  {
    "exchange": "BINANCE",
    "market": "SPOT",
    "symbol": "XRPUSDT",
    "interval": "1h",
    "start": "2020-01-01",
    "end": "2025-01-01"
  }
]

```

Пример файла `optimization.json` доступен в папке `help`. Возможные значения ключей JSON-файла перечислены в файле `json_enums.txt`.

3. Запустите программу в терминале из корневой директории проекта:

```bash
python starter.py
```

### Тестирование

#### Тестирование одной стратегии

1. В файле `config.py` установите значение переменной `MODE`:

```python
MODE = enums.Mode.TESTING
```

2. Укажите параметры тестирования в словаре `TESTING_INFO`:

```python
TESTING_INFO = {
    'exchange': enums.Exchange.BINANCE,
    'market': enums.Market.SPOT,
    'symbol': 'BTCUSDT',
    'interval': '1h',
    'start': '2017-01-01',
    'end': '2019-12-01',
    'strategy': enums.Strategy.NUGGET_V2,
}
```

Возможные значения параметров перечислены в файле `config_enums.txt`.

3. Запустите программу в терминале из корневой директории проекта:

```bash
python starter.py
```

4. Перейдите в браузере по адресу http://127.0.0.1:5000 для просмотра результатов.

#### Тестирование нескольких стратегий

1. В файле `config.py` установите значение переменной `MODE`:

```python
MODE = enums.Mode.TESTING
```

2. Перенесите файлы с оптимальными параметрами из папки `optimization` в папку `backtesting` в соответствующих директориях стратегий. В начало каждого файла можно добавить строку с обновлённым временным периодом (например, `Period: 2017-01-01 - 2019-01-01`).

3. Запустите программу в терминале из корневой директории проекта:

```bash
python starter.py
```

4. Перейдите в браузере по адресу http://127.0.0.1:5000 для просмотра результатов.

### Автоматизация

#### Автоматизация одной стратегии

1. В файле `config.py` установите значение переменной `MODE`:

```python
MODE = enums.Mode.AUTOMATION
```

2. Укажите параметры автоматизации в словаре `AUTOMATION_INFO`:

```python
AUTOMATION_INFO = {
    'exchange': enums.Exchange.BYBIT,
    'symbol': 'BTCUSDT',
    'interval': 1,
    'strategy': enums.Strategy.DEVOURER_V3,
}
```

Возможные значения параметров перечислены в файле `config_enums.txt`.

3. Запустите программу в терминале из корневой директории проекта:

```bash
python starter.py
```

4. Перейдите в браузере по адресу http://127.0.0.1:5000 для просмотра результатов.

#### Автоматизация нескольких стратегий

1. В файле `config.py` установите значение переменной `MODE`:

```python
MODE = enums.Mode.AUTOMATION
```

2. Создайте текстовые файлы автоматизации в соответствующих папках стратегий (например, `TVLite/src/model/strategies/nugget_v2/automation`). Имена файлов должны содержать название биржи, тикер и таймфрейм (например, `BYBIT_BTCUSDT_1.txt`). В файлах укажите параметры стратегии и их значения. Параметры стратегий определены в соответствующих модулях (например, `nugget_v2.py`). Пример файла автоматизации доступен в папке `help`.

3. Запустите программу в терминале из корневой директории проекта:

```bash
python starter.py
```

4. Перейдите в браузере по адресу http://127.0.0.1:5000 для просмотра результатов.

## Дополнительная информация

- Для корректной работы программы требуется стабильное интернет-соединение.
- Рекомендуется регулярно синхронизировать системное время на вашем устройстве.
- Flask-сервер, запускаемый программой, по умолчанию доступен по адресу: http://127.0.0.1:5000.
Для удалённого доступа к Flask-серверу можно настроить туннель, например, с помощью `ngrok`. Полученный URL укажите в файле `config.py`.

---

**Код проекта доступен на платной основе. Свяжитесь со мной для получения доступа.**
