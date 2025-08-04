## Налаштування пошти в Zulip (локальне та SMTP)

 [Встановлення з маркетплейсу DigitalOcean](https://marketplace.digitalocean.com/apps/zulip) 

### Основні команди:

```bash
# Перевірка логів:
cat /var/log/zulip/errors.log
tail -n 100 /var/log/zulip/send_email.log
tail -f /var/log/zulip/send_email.log

# Перевірка сокету SMTP (наприклад, порт 2525 або 587):
telnet yourhostel.kiev.ua <port>

# Журнал системи (Django):
journalctl -u zulip-django -f
journalctl -u zulip-django -n 100

# Тестовий email у файлову систему:
mkdir -p /tmp/zulip-emails
cd /tmp/zulip-emails/
rm -v /tmp/zulip-emails/*

# Редагування конфігурації пошти:
nano /etc/zulip/settings.py

EMAIL_HOST = "mail.adm.tools"
EMAIL_HOST_USER = "admin@domain.mail"
EMAIL_USE_TLS = True
EMAIL_PORT = <port>

# Уникнути помилок із "noreply@host"
ADD_TOKENS_TO_NOREPLY_ADDRESS = False
NOREPLY_EMAIL_ADDRESS = "admin@domain.mail"

# У settings.py для локального тесту:
EMAIL_BACKEND = 'django.core.mail.backends.filebased.EmailBackend'
EMAIL_FILE_PATH = '/tmp/zulip-emails'
RATE_LIMITING = False

# /etc/zulip/zulip-secrets.conf
email_password = <SMTP_PWD>

# Перезапуск Zulip після змін:
 /home/zulip/deployments/current/scripts/restart-server

# Тест надсилання листа:
 /home/zulip/deployments/current/manage.py send_test_email test@domain.mail
```
[Офіційна документація з налаштування email](https://zulip.readthedocs.io/en/latest/production/email.html)
