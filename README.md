# Установка Outline с динамичским ключоии обходом блокировки
## Нам понядобиться доменное имя
### Скачиваем скрипт
```bash
sudo wget https://raw.githubusercontent.com/neon0ff/outline/main/install_server.sh
```
### Делаем его выполняемым
```bash
sudo chmod +x install_server.sh
```
### Запускаем скрипт с параметром хоста
```bash
./install_server.sh --hostname example.com
```
### Если требуется указать порт для ключей в добавок вписываем параметр ```bash
--keys-port```
