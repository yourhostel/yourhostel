```text
ansible/
├── inventory.ini
├── playbook.yml
└── roles/
    └── meshcentral/
        ├── meshcentral-data/
        │   ├── config.json
        │   ├── webserver-cert-public.crt
        │   └── webserver-cert-private.key
        ├── docker-compose.yml
        └── tasks/
            └── main.yml
```

```bash
# admin@yourhostel.kiev.ua
scp root@<IP>:/opt/meshcentral/meshcentral-data/webserver-cert-public.crt \
    ~/Scripts/yourhostel/mesh/ansible/roles/meshcentral/meshcentral-data/

scp root@<IP>:/opt/meshcentral/meshcentral-data/webserver-cert-private.key \
    ~/Scripts/yourhostel/mesh/ansible/roles/meshcentral/meshcentral-data/
```
