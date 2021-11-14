## MySQL
<img alt="Docker" src="https://img.shields.io/badge/Docker-2496ED?&style=flat&logo=docker&logoColor=ffffff">&nbsp;
<img alt="MySql" src="https://img.shields.io/badge/MySql-F7F7F7?&style=flat&logo=mysql&logoColor=336791">&nbsp;

## Description 
Simple template of MySQL with Docker Compose

## Prerequisite
* [Docker](https://docs.docker.com/engine/install/ubuntu/)
* [Docker Compose](https://docs.docker.com/compose/install/)
* [MySQL](https://hub.docker.com/_/mysql)

## Quick Start
```bash
time ./quick-start.sh
```

## Default Value
Create `.env` file to define your own value
| Variable name | Default value | Datatype | Description |
|:--------------|:--------------|:--------:|------------:|
|MYSQL_ROOT_PASSWORD|password|String|Root password|
|MYSQL_USER|user|String|Initial user|
|MYSQL_PASS|password|String|Initial user password|

## Setup
**Step 1:** Add `MySQL` service into your `docker-compose.yml`
```yaml
version: "3.7"

services:
  mysql:
    image: mysql:8.0
    container_name: mysql
    ports:
      - "3306:3306"
    networks:
      - net      
    restart: always          
```

**Step 2:** Add command after start for authentication (Reference MySQL document from docker hub)
```yaml
    command: --default-authentication-plugin=mysql_native_password
```

**Step 3:** Mount volume bind into your server
```yaml
    volumes:
      - mysql_vol:/var/lib/mysql
```

**Step 4:** Set username and password of `MySQL` in environment
```yaml
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD:-password}
      MYSQL_USER: ${MYSQL_USER:-user}
      MYSQL_PASS: ${MYSQL_PASS:-password}
```

**Step 5:** Add the volume description
```yaml
volumes:
  mysql_vol:
    driver: local
```

**Step 6:** Add the network description
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
  mysql:
    image: mysql:8.0
    container_name: mysql
    command: --default-authentication-plugin=mysql_native_password
    ports:
      - "3306:3306"
    volumes:
      - mysql_vol:/var/lib/mysql
    networks:
      - net
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD:-password}
      MYSQL_USER: ${MYSQL_USER:-user}
      MYSQL_PASS: ${MYSQL_PASS:-password}

volumes:
  mysql_vol:
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
* [MySQL](https://hub.docker.com/_/mysql)

## Contributor
<a href="https://github.com/Harin3Bone"><img src="https://img.shields.io/badge/Harin3Bone-181717?style=flat&logo=github&logoColor=ffffff"></a>