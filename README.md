# Скрипт для мониторинга процесса

Этот проект содержит реализацию скрипта Bash для мониторинга процесса `test` в среде Linux, а также необходимые unit-файлы systemd (`mymonitoring.service` и `mymonitoring.timer`) для автоматического запуска скрипта каждую минуту.

## Описание

Проект включает в себя:
*   **Скрипт Bash (`test_monitoring.sh`)**: Основная логика мониторинга процесса `test`.
*   **Systemd Service Unit (`mymonitoring.service`)**: Определяет, как systemd должен выполнять скрипт.
*   **Systemd Timer Unit (`mymonitoring.timer`)**: Настраивает периодический запуск сервиса (каждую минуту).

## Установка

Для корректной работы на вашей системе, следуйте приведенному ниже руководству по установке.

### 1. Клонирование репозитория

Скопируйте репозиторий на свой компьютер с помощью команды:

```bash
git clone https://github.com/yarickmalyshev/monitoring-script.git
```

### 2. Копирование файлов

Перейдите в папку проекта и выполните следующие команды для копирования файлов в нужные системные директории:

```bash
# Копирование скрипта
sudo cp test_monitoring.sh /usr/local/bin/test_monitoring.sh

# Копирование unit-файла сервиса
sudo cp mymonitoring.service /etc/systemd/system/mymonitoring.service

# Копирование unit-файла таймера
sudo cp mymonitoring.timer /etc/systemd/system/mymonitoring.timer
```

### 3. Настройка прав и активация

Сделайте скрипт исполняемым и активируйте systemd-таймер:

```bash
# Сделать скрипт исполняемым
sudo chmod +x /usr/local/bin/test_monitoring.sh

# Перезагрузить конфигурацию systemd, чтобы она увидела новые unit-файлы
sudo systemctl daemon-reload

# Включить таймер (он будет автоматически запускаться при загрузке системы)
sudo systemctl enable mymonitoring.timer

# Запустить таймер немедленно (до перезагрузки)
sudo systemctl start mymonitoring.timer
```

### 4. Проверка состояния

Убедитесь в успешном запуске и работе сервиса с помощью команды:

```bash
sudo systemctl status mymonitoring.timer
```

<img width="1652" height="259" alt="image" src="https://github.com/user-attachments/assets/02283c3f-24c9-42e2-a2f8-fd85866620bd" />


Или для проверки самого сервиса:

```bash
sudo systemctl status mymonitoring.service
```

<img width="2355" height="369" alt="image" src="https://github.com/user-attachments/assets/7dd55587-d0f0-40ab-9ff1-efb885860d93" />


---
