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

**Mozeme vygenerovat `Controller, Model a migration` pomocou jedneho prikazu**

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


####sablony

Sablony su umiestnene v adresari `resources/views`

Na pristup k sablonam pouzivame tzv. dot-notation, namiesto `/` piseme `.`

```php
public function index() {
    $pages = Page::all();

    return view('pages.index', ['pages' => $pages]);
}
```

####requesty - Odosielanie formulara

Odosielanie Formulara

view

```blade
<form action="{{ url('/page') }}" method="post">
    {{ csrf_field() }} {{-- Takto pridavame hidden input pre CSRF token --}}
    <input type="text" name="name">
    <input type="email" name="email">
    <button type="submit">Submit</button>
</form>
```

PageController

```php
use Illuminate\Http\Request;

public function store(Request $request) {
    $user = Auth::user()->id;
    $data = $request->all();

    $data['user_id'] = $user;
    Page::create($data);

    return back();
}
```

*That's all*

**Podrobnosti:**

Trieda `Request` obsahuje POST data, funkciou `all()` dostaneme pole (podobne ako `$_POST`)

Aby zapis `Model::create` fungoval treba definovat v [modeli](./komponenty.html#model) pole `$fillable`!

Aktualne prihlaseny uzivatel (objekt `User`) vieme zistit pomocou `Auth::user()`.
