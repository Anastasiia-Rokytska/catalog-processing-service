# Catalog File Processing Service
## Run

Requirements: Java 21 and Docker (Docker Desktop or another engine).

```bash
docker-compose up -d        # PostgreSQL 16 on localhost:5432, wait until it is "healthy"
docker-compose ps
./mvnw spring-boot:run      # drop files into data/input-folder
./mvnw test                 # starts its own PostgreSQL with Testcontainers
docker-compose down         # stop the DB (add -v to also delete the data volume)
```

- `spring-boot-docker-compose` (dev only) also starts `docker-compose.yml` automatically on `spring-boot:run`,
  so the first command is optional. It is skipped in tests.
- DB settings come from env variables with local defaults: `DB_URL`, `DB_USER`, `DB_PASSWORD` (app) and
  `DB_NAME`, `DB_USER`, `DB_PASSWORD`, `DB_PORT` (compose). The defaults are `catalog` / `catalog` / `catalog`.
- The JVM runs with `-Duser.timezone=UTC` (set in `pom.xml`), because PostgreSQL rejects legacy zone names
  such as `Europe/Kiev`. If you run the app from the IDE, add the same VM option.
