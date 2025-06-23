# MeshCentral
## Встановлення вручну

```text
/opt/meshcentral/
├── docker-compose.yml
├── mongo-data/
├── meshcentral-data/
│   ├── config.json
│   ├── webserver-cert-public.crt
│   └── webserver-cert-private.key
```


```bash
# Генерація сертифікату Buypass (2048-bit RSA)
curl https://get.acme.sh | sh
source ~/.bashrc
acme.sh --set-default-ca --server https://api.buypass.com/acme/directory
curl https://get.acme.sh | sh -s email=admin@yourhostel.kiev.ua # switching
acme.sh --register-account -m admin@yourhostel.kiev.ua --server https://api.buypass.com/acme/directory

apt update && apt install socat -y

acme.sh --issue --standalone -d mesh.yourhostel.kiev.ua --keylength 2048 --server https://api.buypass.com/acme/directory #generate

# Копіюємо сертифікати
cp /root/.acme.sh/mesh.yourhostel.kiev.ua/fullchain.cer \
   /opt/meshcentral/meshcentral-data/webserver-cert-public.crt

cp /root/.acme.sh/mesh.yourhostel.kiev.ua/mesh.yourhostel.kiev.ua.key \
   /opt/meshcentral/meshcentral-data/webserver-cert-private.key

chmod 644 /opt/meshcentral/meshcentral-data/webserver-cert-public.crt
chmod 600 /opt/meshcentral/meshcentral-data/webserver-cert-private.key

Встановлення Docker та запуск MeshCentral
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
docker version
docker compose up -d

dig +short mesh.yourhostel.kiev.ua

# DNS перевірка
https://mesh.yourhostel.kiev.ua/meshagents
```

# Повне очищення Docker
```bash
docker stop $(docker ps -aq)
docker rm $(docker ps -aq)
docker rmi $(docker images -q)
docker volume prune -f
docker system prune -a --volumes -f
```