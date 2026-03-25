# 🛠 Скрипты синхронизации репозиториев

Эта папка содержит готовые скрипты для автоматической синхронизации содержимого между двумя локальными git-репозиториями.

---

## 📁 Файлы в папке

- **[sync_repos.ps1](sync_repos.ps1)** — PowerShell скрипт для Windows систем
- **[sync_repos.sh](sync_repos.sh)** — Bash скрипт для Linux/Unix систем (Ubuntu, WSL, Docker)

---

## 🚀 Быстрый старт

### Windows (PowerShell)

```powershell
.\sync_repos.ps1 -SourceRepoPath "C:\path\to\source\repo" -DestRepoPath "C:\path\to\dest\repo" -DoGitPush
```

### Linux/WSL (Bash)

```bash
chmod +x sync_repos.sh
./sync_repos.sh --source /path/to/source/repo --dest /path/to/dest/repo --push
```

---

## 📋 Полная документация

Полная документация с описанием, требованиями, тестированием и устранением неполадок находится в [главном README.md](../README.md).

---

## 🔙 Вернуться к портфолио

[← Вернуться в портфолио проектов](../README.md)
