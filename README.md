# Demo of how to add `_FILE` into into an enviroment variable in docker secrets (Docker Swarm Mode)
## Use Case
Not to expose the Connection String URI Format of MongoDB in docker compose -https://docs.mongodb.com/manual/reference/connection-string/#connection-string-uri-format

This repo contains an example of how to change `MONGODB_URI` to expose `MONGODB_URI_FILE` instead in docker secret as an environment variable.
This is named throughout the repo as:
```
MONGODB_URI_FILE
```
but anything would work. The example is inspired by how this is implemented in the official MySQL and WordPress images:
- https://github.com/docker-library/mysql/blob/master/5.7/docker-entrypoint.sh
- https://github.com/docker-library/wordpress/blob/master/docker-entrypoint.sh
- https://github.com/adrian-gheorghe/demo-docker-secrets-env-vars

## Initialize Swarm and create a secret
```bash
docker swarm init
printf "mongodb://mongodb0.example.com:27017" | docker secret create mongodburidockersecret -
```

## Clone repo and deploy stack
```bash
git clone https://github.com/reraxe/demo-docker-secrets-env-vars.git demo-docker-secrets-env-vars
cd demo-docker-secrets-env-vars
```
Build images first (For this demo, the images will not be loaded from an external Docker registry) but build from the repo directly
```
docker-compose build
```

Deploy stack and check logs
```bash
docker stack deploy -c docker-compose.yaml secrets --prune
docker service logs secrets_php -f
```

Output should be something along the following lines
```bash
secrets_php.1.odzanf4ar9dw@docker-desktop    | string(21) "mysupersecurepassword"
```
This is because the php container command is set to only run the index.php file included in the folder.

This file contains the following:
```php
<?php

var_dump($_ENV['MONGODB_URI']);
```
