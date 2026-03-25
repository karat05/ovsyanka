# Nginx Web Server в Docker

## Описание

Nginx — высокопроизводительный HTTP-сервер и обратный прокси. Этот документ описывает процесс запуска Nginx контейнера с использованием Docker.

## Требования

- Установленный Docker
- Права на запуск Docker контейнеров
- Доступ в интернет для загрузки образа

---

## Шаг 1: Установка Docker

Если Docker ещё не установлен, выполните следующие команды:

### Windows
```powershell
winget install Docker.DockerDesktop
```

### Linux/WSL
```bash
sudo apt update
sudo apt install docker.io docker-compose
sudo systemctl start docker
sudo systemctl enable docker
```

---

## Шаг 2: Проверка установки Docker

### Windows
```powershell
docker --version
docker ps
```

### Linux/WSL
```bash
docker --version
docker ps
```

![Проверка Docker](images/docker-version.png)

---

## Шаг 3: Поиск образа Nginx

```powershell
# Windows PowerShell
docker search nginx
```

```bash
# Linux/WSL Bash
docker search nginx
```

![Поиск Nginx](images/search-nginx.png)

---

## Шаг 4: Загрузка образа Nginx

### Официальный образ Nginx

```powershell
# Windows PowerShell
docker pull nginx:latest
```

```bash
# Linux/WSL Bash
docker pull nginx:latest
```

![Загрузка образа](images/pull-nginx.png)

### Альтернативный вариант с Alpine (меньший размер)

```powershell
# Windows PowerShell
docker pull nginx:alpine
```

```bash
# Linux/WSL Bash
docker pull nginx:alpine
```

![Загрузка Alpine образа](images/pull-nginx-alpine.png)

---

## Шаг 5: Запуск контейнера Nginx

### Базовый запуск

```powershell
# Windows PowerShell
docker run -d --name my-nginx -p 80:80 nginx:latest
```

```bash
# Linux/WSL Bash
docker run -d --name my-nginx -p 80:80 nginx:latest
```

**Параметры:**
- `-d` — запуск в фоновом режиме (detached)
- `--name my-nginx` — имя контейнера
- `-p 80:80` — проброс портов (хост:контейнер)
- `nginx:latest` — образ Nginx

![Запуск контейнера](images/run-nginx.png)

### Запуск с монтированием локальной папки

```powershell
# Windows PowerShell
docker run -d --name my-nginx -p 80:80 -v ${PWD}/html:/usr/share/nginx/html nginx:latest
```

```bash
# Linux/WSL Bash
docker run -d --name my-nginx -p 80:80 -v $(pwd)/html:/usr/share/nginx/html nginx:latest
```

**Параметры:**
- `-v ${PWD}/html:/usr/share/nginx/html` — монтирование локальной папки в контейнер

![Запуск с монтированием](images/run-nginx-volume.png)

### Запуск с автоматическим перезапуском

```powershell
# Windows PowerShell
docker run -d --name my-nginx -p 80:80 --restart always nginx:latest
```

```bash
# Linux/WSL Bash
docker run -d --name my-nginx -p 80:80 --restart always nginx:latest
```

**Параметры:**
- `--restart always` — автоматический перезапуск контейнера

![Запуск с перезапуском](images/run-nginx-restart.png)

---

## Шаг 6: Проверка работы контейнера

### Проверка статуса контейнера

```powershell
# Windows PowerShell
docker ps
```

```bash
# Linux/WSL Bash
docker ps
```

![Проверка статуса](images/docker-ps.png)

### Проверка логов

```powershell
# Windows PowerShell
docker logs my-nginx
```

```bash
# Linux/WSL Bash
docker logs my-nginx
```

![Логи контейнера](images/docker-logs.png)

### Доступ к веб-серверу

Откройте браузер и перейдите по адресу:
- `http://localhost` или
- `http://127.0.0.1`

Вы должны увидеть страницу приветствия Nginx:

![Страница Nginx](images/nginx-welcome.png)

---

## Шаг 7: Создание собственного сайта

### Создание HTML файла

Создайте файл `index.html` в локальной папке:

```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Мой сайт на Nginx</title>
</head>
<body>
    <h1>Добро пожаловать на мой сайт!</h1>
    <p>Это тестовый сайт запущенный в Docker контейнере.</p>
    <p>Веб-сервер: Nginx</p>
</body>
</html>
```

### Запуск контейнера с собственным сайтом

```powershell
# Windows PowerShell
docker run -d --name my-nginx -p 80:80 -v ${PWD}/html:/usr/share/nginx/html nginx:latest
```

```bash
# Linux/WSL Bash
docker run -d --name my-nginx -p 80:80 -v $(pwd)/html:/usr/share/nginx/html nginx:latest
```

![Собственный сайт](images/custom-site.png)

---

## Шаг 8: Создание конфигурации Nginx

### Создание собственного конфига

Создайте файл `nginx.conf`:

```nginx
server {
    listen 80;
    server_name localhost;
    
    location / {
        root /usr/share/nginx/html;
        index index.html index.htm;
    }
    
    location /api {
        proxy_pass http://backend:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### Запуск с собственным конфигом

```powershell
# Windows PowerShell
docker run -d --name my-nginx -p 80:80 -v ${PWD}/nginx.conf:/etc/nginx/nginx.conf nginx:latest
```

```bash
# Linux/WSL Bash
docker run -d --name my-nginx -p 80:80 -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf nginx:latest
```

![Собственный конфиг](images/custom-config.png)

---

## Шаг 9: Управление контейнером

### Остановка контейнера

```powershell
# Windows PowerShell
docker stop my-nginx
```

```bash
# Linux/WSL Bash
docker stop my-nginx
```

### Запуск остановленного контейнера

```powershell
# Windows PowerShell
docker start my-nginx
```

```bash
# Linux/WSL Bash
docker start my-nginx
```

### Перезапуск контейнера

```powershell
# Windows PowerShell
docker restart my-nginx
```

```bash
# Linux/WSL Bash
docker restart my-nginx
```

### Удаление контейнера

```powershell
# Windows PowerShell
docker rm my-nginx
```

```bash
# Linux/WSL Bash
docker rm my-nginx
```

---

## Шаг 10: Работа с файлами в контейнере

### Вход в контейнер

```powershell
# Windows PowerShell
docker exec -it my-nginx /bin/bash
```

```bash
# Linux/WSL Bash
docker exec -it my-nginx /bin/bash
```

![Вход в контейнер](images/docker-exec.png)

### Копирование файлов в контейнер

```powershell
# Windows PowerShell
docker copy index.html my-nginx:/usr/share/nginx/html/
```

```bash
# Linux/WSL Bash
docker cp index.html my-nginx:/usr/share/nginx/html/
```

![Копирование файлов](images/docker-cp.png)

### Копирование файлов из контейнера

```powershell
# Windows PowerShell
docker cp my-nginx:/usr/share/nginx/html/index.html index.html
```

```bash
# Linux/WSL Bash
docker cp my-nginx:/usr/share/nginx/html/index.html index.html
```

---

## Шаг 11: Просмотр информации о контейнере

### Информация о контейнере

```powershell
# Windows PowerShell
docker inspect my-nginx
```

```bash
# Linux/WSL Bash
docker inspect my-nginx
```

![Инспекция контейнера](images/docker-inspect.png)

### Использование ресурсов

```powershell
# Windows PowerShell
docker stats my-nginx
```

```bash
# Linux/WSL Bash
docker stats my-nginx
```

![Статистика ресурсов](images/docker-stats.png)

---

## Шаг 12: Удаление образа

### Просмотр загруженных образов

```powershell
# Windows PowerShell
docker images
```

```bash
# Linux/WSL Bash
docker images
```

### Удаление образа

```powershell
# Windows PowerShell
docker rmi nginx:latest
```

```bash
# Linux/WSL Bash
docker rmi nginx:latest
```

![Удаление образа](images/docker-rmi.png)

---

## Полезные команды Docker

### Список всех контейнеров
```bash
docker ps -a
```

### Просмотр логов в реальном времени
```bash
docker logs -f my-nginx
```

### Поиск контейнеров
```bash
docker ps | findstr nginx
```

### Очистка неиспользуемых контейнеров
```bash
docker container prune
```

### Очистка неиспользуемых образов
```bash
docker image prune
```

---

## Сравнение Apache и Nginx

| Характеристика | Apache | Nginx |
|---------------|--------|--------|
| Архитектура | Многопоточная, на основе процессов | Событийная, асинхронная |
| Производительность | Хорошая для PHP/Perl | Высокая для статического контента |
| Конфигурация | .htaccess, Apache config | nginx.conf |
| Память | Больше | Меньше |
| Простота настройки | Простая | Требует понимания |
| Поддержка Windows | Отличная | Хорошая |

---

## Troubleshooting

### Порт 80 уже занят

Если получаете ошибку о занятом порту, используйте другой порт:

```powershell
docker run -d --name my-nginx -p 8080:80 nginx:latest
```

Затем доступ к сайту через: `http://localhost:8080`

### Контейнер не запускается

Проверьте логи:

```bash
docker logs my-nginx
```

### Нет доступа к сайту

Проверьте, что контейнер запущен:

```bash
docker ps
```

Проверьте фаервол Windows/антивирус, если он блокирует порт 80.

### Конфликт портов с Apache

Если Apache использует порт 80, остановите его:

```bash
docker stop my-apache
```

---

## Дополнительные ресурсы

- [Официальная документация Nginx](https://nginx.org/en/docs/)
- [Официальный образ Nginx на Docker Hub](https://hub.docker.com/_/nginx)
- [Документация Docker](https://docs.docker.com/)

---

## Пример с Apache для сравнения

Для справки можно посмотреть [пример запуска Apache контейнера](../Apache.md).

---

> **Примечание:** При работе с Docker избегайте использования русских символов в именах файлов и папок, а также пробелов и спецсимволов.
