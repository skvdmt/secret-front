# secret-front

### Trandlations

[En](./README.md)

### Описание

Для получения секретного текста от бэкенд-API через фронтенд-приложение требуется аутентификация.

Приложение работает в связке с тримя бекэнд приложениями.

В [auth-back](https://github.com/skvdmt/auth-back) выдаеются токены доступа после Basic аутентификауции. А также выдает новую пару токенов по токену обновления.

Приложение [secret-back](https://github.com/skvdmt/secret-back) требует токен доступа для Bearer аутентификации и соединяется по gRPC с приложениев прверяющим токен доступа.

Приложение [valid-access-token](https://github.com/skvdmt/valid-access-back) проводит валидацию токена доступа на бэкенде.

### Скачать

```sh
git clone https://github.com/skvdmt/secret-front
```

### Ссылки

- [Пример](https://secret.skvdmt.ru/) — Пример работы фронтенд-приложения.
- [Исходник](https://github.com/skvdmt/secret-front) — Исходный код фронтенд-приложения.
- [Образ Docker](https://hub.docker.com/r/skvdmt/secret-front) — Образ Docker на docker hub.
- [Исходник backend API аутентификации](https://github.com/skvdmt/auth-back) — Исходный код backend приложения аутентификации.
- [Исходник backend API секрета](https://github.com/skvdmt/secret-back) — Исходный код backend приложения получения секрета.
- [Исходник backend проверки токена доступа](https://github.com/skvdmt/valid-access-back) — Исходный код backend приложения проверки токена доступа.
- [Скиданов Дмитрий](https://skvdmt.ru) — Автор.
