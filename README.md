## Minimal reproducer for API Platform issue

See [issue #6831](https://github.com/api-platform/core/issues/6831)

### Steps to reproduce

1. Clone this repository
2. Launch in production mode:
   ```bash
   SERVER_NAME=localhost POSTGRES_PASSWORD='!ChangeMe!' APP_SECRET='foobat' APP_ENV=prod CADDY_MERCURE_JWT_SECRET=ChangeThisMercureHubJWTSecretKey  docker compose -f compose.yaml -f compose.prod.yaml up -d --build
   ```
3. Shell in to the PHP container and generate a JWT keypair:
   ```bash
   docker compose exec php bash
   bin/console lexik:jwt:generate-keypair
   ```
4. Visit https://localhost in your browser.
5. Use the auth endpoint to authenticate with the email `user@localhost` and password `password`.
6. Try the greetings endpoint, setting `name` to an empty string `""`.
7. See the 422 response and validation error.
8. Immediately try to send a request to the auth endpoint and see it fail with a 404 response.
