[Laravel](./index.html)
=======================

[< Laravel komponenty](./komponenty.html)

- - - -

## Laravel CRUD app

#### homestead

```bash
homestead up
homestead ssh
```

####pridavanie aplikacie

```bash
cd /www
laravel new super-app
```

####konfiguracia DB

**Konfiguracia je v `.env` v hlavnom adresari aplikacie**

```php
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret
```

####generovanie kodu (make)

**Mozeme vygenerovat MVC pomocou prikazu**

 - -m    migracia
 - -c    controller
 - -r    resource (CRUD)

```bash
artisan make:model -mcr Page
```

Vygenerovane subory:

```
database/migrations/create_pages_table
app/Page.php #model
app/Http/Controllers/PageController.php
```

5. sablony

...

6. requesty

...
