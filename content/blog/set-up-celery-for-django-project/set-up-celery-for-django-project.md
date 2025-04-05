---
title: Set up Celery production for Django project
description: Set up Celery for a Django project on production with services to serve for the crob job
date: 2025-04-05
tags:
  - experience
  - django
og_image: set-up-celery-for-django-project.webp
pageType: blog
---
## 🚀 Background

Celery is a **cron job service** commonly used in Django projects. In my case, I used Celery to **reset user streaks at midnight (00:00 AM)** for my application.

![Set up the Celery for django project](set-up-celery-for-django-project.webp)

In development, I had to run three terminal windows:

- One for the Django server: `python manage.py runserver`
    
- One for the Celery worker: `celery -A proj worker`
    
- One for the Celery beat: `celery -A proj beat`
    

That setup was a bit complex. So in this blog, I’ll share **how I set up Celery as a production-ready service** using `systemd`.

---

## 🛠️ Approach

When I first moved my app to production, I used **Gunicorn** to serve Django, but forgot about Celery. As a result, scheduled tasks didn’t run because **both Celery Worker and Celery Beat need to run in parallel**.

### ✅ Option 1: Using tmux

Initially, I used `tmux`:

1. SSH into the server.
    
2. Start a `tmux` session and split the window with `Ctrl + b` → `%`.
    
3. Run the worker and beat processes in separate panes.
    

Even after closing SSH, the processes stayed alive (confirmed using `htop`). This works, but it’s not ideal for long-term use.

### ✅ Option 2: Using systemd Services

When I got a new VPS, I wanted a better solution. After some research (and help from ChatGPT 😄), I found a reliable approach using `systemd` services to run Celery in the background.

Reference: [Django with Celery in Production](https://dev.to/iamtekson/django-with-celery-in-production-cb5)

---

## ⚙️ 1. Create the Celery Worker Service

Create a new service file:

```bash
sudo nano /etc/systemd/system/celery.service
```

Paste the following (replace `user`, paths, and `[celery_app]` accordingly):

```ini
[Unit]
Description=Celery Worker Service
After=network.target

[Service]
Type=simple
User=your_username
Group=your_username
WorkingDirectory=/home/your_username/your_project
ExecStart=/home/your_username/.local/share/virtualenvs/your-venv/bin/celery -A [celery_app] worker --loglevel=INFO
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

👉 Replace:

- `your_username` with your actual Linux username.
    
- `[celery_app]` with the value from your `celery.py` file.
    

Then run:

```bash
sudo systemctl daemon-reload
sudo systemctl enable celery
sudo systemctl start celery
```

---

## 🕒 2. Create the Celery Beat Service

Now create the Beat service:

```bash
sudo nano /etc/systemd/system/celery-beat.service
```

Paste the following:

```ini
[Unit]
Description=Celery Beat Service
After=network.target

[Service]
Type=simple
User=your_username
Group=your_username
WorkingDirectory=/home/your_username/your_project
ExecStart=/home/your_username/.local/share/virtualenvs/your-venv/bin/celery -A [celery_app] beat --loglevel=INFO
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Then run:

```bash
sudo systemctl daemon-reload
sudo systemctl enable celery-beat
sudo systemctl start celery-beat
```

✅ Check status:

```bash
sudo systemctl status celery-beat
```

If you see `active (running)`, it means everything is set up correctly.

---

## 🧾 Conclusion

That’s how I set up Celery and Celery Beat in production using `systemd`. It’s a clean, reliable, and maintainable way to manage background tasks in Django.

📚 References:

- [Post by Tek Kshetri](https://dev.to/iamtekson/django-with-celery-in-production-cb5)
    
- [Celery Documentation](https://docs.celeryq.dev/en/stable/getting-started/introduction.html)
    

Thanks for reading! 🙏 Hope this helps you in your deployment journey.