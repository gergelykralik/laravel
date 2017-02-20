[Laravel](./index.html)
=======================

[< Vyvojove prostredie](./prostredie.html)

- - - -

## Inicializacia Laravelu a konfiguracia prostredia

**prikazy spustime na Vagrant VM `homestead`**

```bash
homestead up
homestead ssh
```

### Instalacia (Laravel, PHP Code Sniffer, PHP Mess Detector, etc.)

Globalna instalacia je dostupna pre kazdy projekt.

```bash
composer global require "laravel/installer"
composer global require "squizlabs/php_codesniffer"
composer global require "phpmd/phpmd"
```

#### Novy Laravel projekt

```bash
laravel new nazov-projektu
```

**Takto vytvoreny projekt je vopred nakonfigurovana.**

### Struktura projektu

```
app/Http/Controllers/    # Kontroller
app/Http/Requests/       # Vsetky requesty su presmerovane cez tieto triedy (je mozne pridat kontroly, etc.)
app/Providers            # Service Providers - magic, cez tieto su globalne dostupne funkcie (napr. session)
app/                     # Models
## Konfiguracia
config/app.php           # Konfig subor kniznice, doplna konfig v `.env`
database/migrations/     # Struktura databazy, pripadne zmeny
public                   # Document root
resources                # Kompilovatelne dynamicke subory (sass, less, js, etc.)
views                    # Sablony
routes/web.php           # Router
.env                     # Konfig subor
.gitignore               #
artisan                  #
```

### Interakcia s Laravelom (Artisan)

```bash
cd /path/to/projekt
artisan list             # zoznam prikazov
artisan down             # maintenance mode
artisan up               # prevadzka
artisan optimize         # optimalizacia generovaneho kodu
artisan migrate          # spustenie DB migracii

## Generatory ##
artisan make:auth        # Scaffold basic login and registration views and routes
artisan make:controller  # Create a new controller class
artisan make:migration   # Create a new migration file
artisan make:model       # Create a new Eloquent model class
artisan make:policy      # Create a new policy class
artisan make:provider    # Create a new service provider class
artisan make:request     # Create a new form request class
        
## Router ##
php artisan route:cache  # Create a route cache file for faster route registration
php artisan route:clear  # Remove the route cache file
php artisan route:list   # List all registered routes
```

#### `artisan` - Migracie

```bash
cd /www/laravel-admin

# Vytvaranie tabulky
artisan make:migration create_nazovtabulky_table

# Editacia tabulky
artisan make:migration add_field_nazovpola_to_nazovtabulky_table --TABLE=nazovtabulky
```

- - - -

[Laravel komponenty >](./komponenty.html)