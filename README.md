# wiki-js-example
Using Wiki.js for a simple Enterprise collaboration system

https://wiki.js.org/ seems to be a great alternative to the big costy enterprise collaboration systems... So simply start the setup using Compose with

```shell
docker-compose up -d
```

Access your Wiki at http://localhost:3000

# Install with Docker Compose

See https://docs.requarks.io/install/docker 

```yaml
version: "3"
services:

  db:
    image: postgres:11-alpine
    environment:
      POSTGRES_DB: wiki
      POSTGRES_PASSWORD: wikijsrocks
      POSTGRES_USER: wikijs
    logging:
      driver: "none"
    restart: unless-stopped
    volumes:
      - db-data:/var/lib/postgresql/data

  wiki:
    image: requarks/wiki:2
    depends_on:
      - db
    environment:
      DB_TYPE: postgres
      DB_HOST: db
      DB_PORT: 5432
      DB_USER: wikijs
      DB_PASS: wikijsrocks
      DB_NAME: wiki
    restart: unless-stopped
    ports:
      - "80:3000"

volumes:
  db-data:
```