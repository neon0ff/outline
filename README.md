# Установка Outline с динамическим ключом и обходом блокировки
## Нам потребуется доменное имя
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
sudo ./install_server.sh --hostname example.com
```
### Если требуется указать порт для ключей в добавок вписываем параметр ```--keys-port```
### Далее скачиваем Snap
```bash
sudo apt install snap
```
### Далее скачиваем Certbot
```bash
sudo snap install --classic certbot
```
### Выполняем следующую инструкцию
```bash
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
### Скачиваем Nginx
```bash
sudo apt install nginx
```
### Ставим сертификат
```bash
sudo certbot --nginx
```
### Редактируем конфиг
```bash
sudo nano /etc/nginx/sites-available/default
```
### Переходим на 118 строку комбинацией клавиш ```Ctrl + /``` и редактируем чтобы было как ниже
```bash
        location / {
                add_header Access-Control-Allow-Origin *;
                allow all;
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
        }
```
### Далее смотрим данные ключей и записывем их
```bash
sudo nano /opt/outline/persisted-state/outline-ss-server/config.yml
```
### После чего создаем json файл
```bash
sudo nano /var/www/html/vpn.json
```
### Далее заполняем его в таком формате, соответственно заполнив 3 первые строки своими данными
```bash
{
  "server": "example.cpm",
  "server_port": "keys_port",
  "password": "key_passwod",
  "method": "chacha20-ietf-poly1305",
  "prefix": "\u0016\u0003\u0001\u0000\u00a8\u0001\u0001"
}
```
### Рестартаем Nginx
```bash
sudo systemctl restart nginx.service
```
### Дальше заходим на наш домен и убеждаемся что можем открыть json. Ссылка в нашем случае будет выглядеть примерно так
### https://example.com/vpn.json
### Нам остается переделать ссыку под формат ssconf://example.com/vpn.json и вбить её в Outline Client
