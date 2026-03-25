# Apache в Docker

## Шаг 1: Загрузка образа Apache

```powershell
docker pull httpd:latest
```

**Здесь вставьте скриншот:**
*![Скриншот загрузки образа](images/pull-apache.png)*

---

## Шаг 2: Запуск контейнера

```powershell
docker run -d --name my-apache -p 80:80 httpd:latest
```

**Здесь вставьте скриншот:**
*![Скриншот запуска контейнера](images/run-apache.png)*

---

## Шаг 3: Проверка работы

```powershell
docker ps
```

**Здесь вставьте скриншот:**
*![Скриншот списка контейнеров](images/docker-ps.png)*

---

## Шаг 4: Доступ к веб-серверу

Откройте браузер и перейдите по адресу: `http://localhost`

**Здесь вставьте скриншот:**
*![Скриншот страницы Apache](images/apache-welcome.png)*

---

## Шаг 5: Остановка контейнера

```powershell
docker stop my-apache
```

**Здесь вставьте скриншот:**
*![Скриншот остановки](images/stop-apache.png)*

---

## Шаг 6: Запуск снова

```powershell
docker start my-apache
```

**Здесь вставьте скриншот:**
*![Скриншот запуска](images/start-apache.png)*

---

## Шаг 7: Удаление контейнера

```powershell
docker rm my-apache
```

**Здесь вставьте скриншот:**
*![Скриншот удаления](images/rm-apache.png)*
