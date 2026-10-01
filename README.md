# secret-front

### Translations

[Русский](./README_ru.md)

### Description

Fronted application to getting secret text from backend api require authentication.

The application works in conjunction with three backend applications.

The [auth-back](https://github.com/skvdmt/auth-back) application issues access tokens following Basic authentication and provides a new token pair using a refresh token.

The [secret-back](https://github.com/skvdmt/secret-back) application requires an access token for Bearer authentication and connects via gRPC to the application that validates the access token.

The [valid-access-token](https://github.com/skvdmt/valid-access-back) application performs access token validation on the backend.

### Download

```sh
git clone https://github.com/skvdmt/secret-front
```

### Links

- [Example](https://secret.skvdmt.ru/) — Example of a frontend application in action.
- [Source](https://github.com/skvdmt/secret-front) — Frontend application source code.
- [Docker image](https://hub.docker.com/r/skvdmt/secret-front) — Docker image on docker hub.
- [Auth backend API source](https://github.com/skvdmt/auth-back) — Source code for the authentication backend application.
- [Secret backend API source](https://github.com/skvdmt/secret-back) — Source code for the secret-retrieval backend application.
- [Validation Access Token backend source](https://github.com/skvdmt/valid-access-back) — Source code for the access token validation backend application.
- [Dmitry Skidanov](https://skvdmt.ru) — Author.
