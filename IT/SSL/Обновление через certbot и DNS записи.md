
```bash
certbot certonly --manual --agree-tos --preferred-challenges=dns -d 'kottofey.ru' -d '*.kottofey.ru' --server https://acme-v02.api.letsencrypt.org/directory
```


Заходим на сервер мейн под рутом, вводим команду выше. Перезапускаем nginx 
```shell
nginx -s reload
```
