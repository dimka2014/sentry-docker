# Sentry docker-compose.yml

Docker-compose file for sentry.

## Generate secret-key
```
docker run --rm sentry config generate-secret-key
```
## Create .env file based on .env-default
```
cp .env-default .env
```
## Create directory for postgres data volume
```
mkdir data
```
## Start docker-compose
```
docker-compose -f docker-compose.yml -f docker-compose.exposed.yml up -d
```
## Initialize tables & create initial user
```
source .env
docker run -it --rm -e SENTRY_SECRET_KEY="$SECRET_KEY" -e SENTRY_REDIS_HOST=sentry-redis -e SENTRY_POSTGRES_HOST=sentry-postgres -e SENTRY_DB_USER=$POSTGRES_USER -e SENTRY_DB_PASSWORD=$POSTGRES_PASSWORD --net sentrydocker_default sentry upgrade
```
