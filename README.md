![image](https://github.com/user-attachments/assets/bf3b6c99-52f8-4718-a704-4874d331bf50)


# Nmap Automation Framework

**Nmap Automation Framework** —это улучшенный Python-скрипт для автоматизации сетевого сканирования с использованием `nmap`. Данный инструмент разработан для этичных хакеров, системных администраторов и специалистов по сетевой безопасности и поддерживает асинхронное и запланированное сканирование, удаленное управление через API, шифрование результатов и уведомления через Telegram.

## Основные возможности

- Асинхронное и запланированное сканирование (в том числе SYN, TCP, UDP, OS detection, Aggressive и Ping).
- API для удаленного запуска сканирования через Flask.
- Поддержка шифрования результатов (AES), сохранение данных в зашифрованных файлах.
- Telegram уведомления о завершении сканирования или при ошибках.
- Гибкая настройка через аргументы командной строки.
- Логирование событий для упрощения мониторинга и диагностики.
- Валидация IP-адресов перед запуском.

## Установка

1. Клонируйте репозиторий:
    ```bash
    git clone https://github.com/NazGaf/Nmap-Automation-Framework.git
    cd nmap-automation-framework
    ```

2. Установите зависимости:
    ```bash
    pip install -r requirements.txt
    ```

3. Создайте файл `.env` в корне проекта для хранения конфиденциальных данных (например, токенов):
    ```plaintext
    TELEGRAM_TOKEN=your_telegram_bot_token
    CHAT_ID=your_telegram_chat_id
    ENCRYPTION_KEY=your_generated_encryption_key
    ```

4. Настройте Telegram-бота, добавьте его токен в `.env` и укажите ключ шифрования (ENCRYPTION_KEY), который нужно сгенерировать при первом запуске и сохранить для расшифровки данных.

## Быстрый запуск

Для быстрого запуска скрипта выполните:
```bash
python scan_automation.py
```
Скрипт начнет асинхронное сканирование заданных IP-адресов и поднимет API-сервер для удаленного управления сканированием.

## Использование

**Запуск с параметрами**

Скрипт поддерживает параметры командной строки для гибкого использования:

- `--target` - IP адрес или диапазон для сканирования.
- `--scan_type` - Тип сканирования (`SYN`, `TCP`, `UDP`, `Aggressive`, `OS`, `Ping`).
- `--save_format` - Формат для сохранения результатов (`json`, `csv`).
- `--interval` - Интервал сканирования в минутах для запланированного сканирования.
- `--async` - Использовать асинхронное сканирование.

**Пример:**
```bash
python scan_automation.py --target 192.168.1.1 --scan_type TCP --save_format csv --interval 30 --async
```
## API для удаленного запуска сканирования

API позволяет запускать сканирование удаленно через HTTP-запросы.

**Пример запроса для запуска сканирования:**
```bash
curl -X POST http://localhost:5000/scan -H "Content-Type: application/json" -d '{"target": "192.168.1.1", "scan_type": "TCP"}'
```
Ответ API вернет результат сканирования в формате JSON.

Telegram уведомления
Бот Telegram отправляет уведомления при завершении каждого сканирования и сообщает об ошибках. Для работы этой функции необходимо задать переменные `TELEGRAM_TOKEN` и `CHAT_ID` в файле `.env`.

## Шифрование результатов

Все результаты сканирования автоматически сохраняются в зашифрованном виде (AES) и хранятся в папке `encrypted_results`.

Для расшифровки файлов можно использовать функцию `decrypt_results` в коде:

```python
decrypted_data = decrypt_results("encrypted_results/filename.json")
print(decrypted_data)
```

## Логирование

События, такие как ошибки или успешные сканирования, записываются в файл `scan_log.txt` с меткой времени.

**Структура проекта**

```bash
- `scan_automation.py - основной скрипт для запуска сканирования.
- `encrypted_results/ - директория для сохранения зашифрованных результатов.
- `scan_log.txt - журнал событий и ошибок.
- `requirements.txt - список зависимостей.
- `.env - конфиденциальные данные, такие как токены и ID чата.
```

## Примеры

Запуск асинхронного сканирования для нескольких целей:

```bash
python scan_automation.py --target 192.168.1.1/24 --scan_type UDP --async
```

**Планирование периодического сканирования**:

Запустит сканирование 192.168.1.1 с интервалом в 30 минут и сохранит результат в формате JSON.
```bash
python scan_automation.py --target 192.168.1.1 --scan_type SYN --interval 30 --save_format json
```

**Получение уведомлений в Telegram при завершении сканирования**

В `.env` укажите токен бота и ID чата.
Запустите скрипт с любыми параметрами — уведомления будут отправляться автоматически.

## Требования

-Python 3.7+
-`nmap` должен быть установлен и доступен из командной строки.
Установите `nmap`, если его нет на вашем компьютере:

```bash
sudo apt-get install nmap  # для Ubuntu/Debian
brew install nmap          # для macOS
```

## Примечания

Этот инструмент предназначен для использования в рамках этичного хакинга и должен применяться только к тем сетям, к которым у вас есть разрешение на доступ. Несанкционированное сканирование может быть незаконным в зависимости от местных законов. Автор не несет никакой юридической ответственности за использование данного инструмента. Использование производится на свой собственных страх и риск.

## Рекомендуется использование: AnonSurf

**Также помним, Telegram передает все данные пользователя спец службам, по запросу!**
