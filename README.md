# Official requirements for running application

## Platform
* `php >= 7.2` (served best with `FPM`)
* `MySQL` database backend
* `Redis` database backend

## Run configuration
Application entrypoint is `public/index.php`, all the requests must be marshalled here.
When running application rely on environment variables. Initial subset of variables is expected in `.env` located
in project root. `.env.dist` can be used as a blueprint. 

## Database
Application uses MySQL and Redis as storage backends.

#### Migration
```shell script
$ php artisan migrate --force
```
Rollback failed migration:
```
$ php artisan migrate:rollback --force
```

#### Seeding command
*Usually takes place upon first deployment to populate DB with initial values*
```shell script
$ php artisan db:seed --force
```

### API

* RPC `[GET] /ping` - health check endpoint must return 200 OK if service is configured
* REST resource `/polls` - polls CRUD
* RPC `[POST] /polls/{id}/vote` - to vote in defined poll
* RPC `[GET] /polls/{id}/results` - poll results
* RPC `[GET] /summary` - polls summary

### CLI

```
# Periodic collect to aggregate polls statustics which will be used in /summary API endpoint
$ php artisan polls:collect:status

# Running unit tests
$ php vendor/bin/phpunit -c phpunit.xml 
```
---
# Task 28. Compose. Запуск compose со сборкой образа