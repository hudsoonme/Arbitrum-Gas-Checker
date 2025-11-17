# Arbitrum Gas Checker + Telegram Alerts

Простой и быстрый чекер цены газа в сети **Arbitrum One** с мгновенными уведомлениями в Telegram, когда газ падает ниже заданного порога.

Идеально для снайперов, мемкоин-охотников и всех, кто ждёт дешёвый газ на Arbitrum!

## 🚀 Особенности

- Обновление каждые **5–6 секунд**
- Уведомления только при падении газа ниже порога (настраивается)
- Уведомление, когда газ снова вырос
- Минимальная нагрузка на систему
- Работает **24/7** на VPS, Render, Railway, Fly.io или домашнем ПК

---

## 📦 Установка и запуск

### 1. Клонирование репозитория

```bash
git clone https://github.com/hudsoonme/arbitrum-gas-checker.git
cd arbitrum-gas-checker
```

---

### 2. Создание виртуального окружения и установка зависимостей

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

---

### 3. Настройка `.env`

```bash
cp .env.example .env
nano .env
```

Пример содержимого:

```
TELEGRAM_BOT_TOKEN=123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11
TELEGRAM_CHAT_ID=-1001234567890
GAS_THRESHOLD_GWEI=0.5        # ниже какого газа отправлять алерт (Arbitrum обычно 0.1–1 gwei)
CHECK_INTERVAL=6              # интервал проверки
```

---

### 4. Как создать Telegram-бота и получить chat_id

1. Откройте Telegram → найдите **@BotFather**  
2. Команда `/newbot` → придумайте имя и username  
3. Скопируйте токен (формата `123456:ABC-...`)  
4. Напишите своему боту любое сообщение или добавьте его в канал  
5. Узнайте `chat_id`:

```
https://api.telegram.org/bot<ВАШ_ТОКЕН>/getUpdates
```

или просто используйте **@userinfobot**

---

### 5. Запуск

```bash
python checker.py
```

После запуска в Telegram придёт сообщение:

**"Arbitrum Gas Checker запущен"**

---

## 🟢 Запуск 24/7 (рекомендуется)

### Вариант 1 — через `screen` (самое простое)

```bash
screen -S arbitrumgas
python checker.py
```

Отсоединиться: **Ctrl + A**, затем **D**  
Вернуться:

```bash
screen -r arbitrumgas
```

---

### Вариант 2 — через `systemd` (идеально для VPS)

Создаём сервис:

```bash
sudo nano /etc/systemd/system/arbitrumgas.service
```

Содержимое файла (замените пути на свои):

```ini
[Unit]
Description=Arbitrum Gas Checker with Telegram Alerts
After=network.target

[Service]
WorkingDirectory=/home/user/arbitrum-gas-checker
ExecStart=/home/user/arbitrum-gas-checker/venv/bin/python /home/user/arbitrum-gas-checker/checker.py
Restart=always
RestartSec=10
User=user
Environment=PYTHONUNBUFFERED=1

[Install]
WantedBy=multi-user.target
```

Активация:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now arbitrumgas.service
```

Проверка:

```bash
sudo systemctl status arbitrumgas.service
journalctl -u arbitrumgas.service -f
```

---

## 🎉 Готово!

Теперь ты всегда будешь знать, когда газ на **Arbitrum** дешёвый — можно снайпить!!!

Автор: **[@margo_hud](https://x.com/margo_hud)**

      
    
    



