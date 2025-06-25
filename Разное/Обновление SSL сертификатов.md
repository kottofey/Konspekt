# DNS записи в терминале

```bash
dig sphere-training.ru TXT +noall +answer
```

# Обновление через certbot и DNS записи

```bash
certbot certonly --manual --agree-tos --preferred-challenges=dns -d 'kottofey.ru' -d '*.kottofey.ru' --server https://acme-v02.api.letsencrypt.org/directory
```
