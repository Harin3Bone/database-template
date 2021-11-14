## PostgreSQL
<img alt="Docker" src="https://img.shields.io/badge/Docker-2496ED?&style=flat&logo=docker&logoColor=ffffff">&nbsp;
<img alt="PostgreSql" src="https://img.shields.io/badge/Postgresql-F7F7F7?&style=flat&logo=postgresql&logoColor=336791">&nbsp;

## Description 
Simple template of PostgreSQL with Docker Compose

## Prerequisite
* [Docker](https://docs.docker.com/engine/install/ubuntu/)
* [Docker Compose](https://docs.docker.com/compose/install/)
* [Postgresql](https://hub.docker.com/_/postgres)

## Quick Start
```bash
time ./quick-start.sh
```

## Default Value
Create `.env` file to define your own value
| Variable name | Default value | Datatype | Description |
|:--------------|:--------------|:--------:|------------:|
|POSTGRES_USER|postgres|String|Initial username|
|POSTGRES_PASSWORD|password|String|Initial password|
|TIMEZONE|"Asia/Bangkok"|String|Database Locale Time|

## Setup
**Step 1:** Add `PostgreSql` service into your `docker-compose.yml`
```yaml       
version: "3.7"

services:
  postgres:
    image: postgres:13.5
    container_name: postgres
    ports:
      - "5432:5432"
    networks:
      - net
    restart: always
```

**Step 2:** Mount volume bind into your server
```yaml
    volumes:
      - ./postgresql.conf:/etc/postgresql.conf
      - postgres_vol:/var/lib/postgresql/data
```

**Step 3:** Set username and password of `PostgreSql` in environment
```yaml
    environment:
      POSTGRES_USER: ${POSTGRES_USER:-postgres}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-password}
      TZ: ${TIMEZONE:-"Asia/Bangkok"}
```

**Step 4:** Add the volume description
```yaml
volumes:
  postgres_vol:
    driver: local
```

**Step 5:** Add the network description
```yaml
networks:
  net:
    external: false
    driver: bridge
```

Then `docker-compose.yml` will look like this
```yaml
version: "3.7"

services:
  postgres:
    image: postgres:13.5
    container_name: postgres
    ports:
      - "5432:5432"
    volumes:
      - ./postgresql.conf:/etc/postgresql.conf
      - postgres_vol:/var/lib/postgresql/data
    networks:
      - net
    restart: always
    environment:
      POSTGRES_USER: ${POSTGRES_USER:-postgres}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-password}
      TZ: ${TIMEZONE:-"Asia/Bangkok"}

volumes:
  postgres_vol:
    driver: local

networks:
  net:
    external: false
    driver: bridge

```

**Step 7:** Start server
```bash
docker-compose up -d
```

## Reference
* [PostgreSQL](https://hub.docker.com/_/postgres)

## Contributor
<a href="https://github.com/Harin3Bone"><img src="https://img.shields.io/badge/Harin3Bone-181717?style=flat&logo=github&logoColor=ffffff"></a>