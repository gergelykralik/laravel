[Laravel](./index.html)
=======================

[< Inicializacia a konfiguracia](./inicializacia.html)

- - - -

## Komponety

Laravel pouziva `singular` pri nazve v PHP, ale `plural` v databaze. Napr. v DB tabulka `posts`, model `Post` a controller `PostController`.

### route

Umiestnenie: `project-root/routes/web.php`

#### Syntax

```php
Route::~requesttype~('~route~', '~resource~');

// Jednoduchy priklad
Route::get('/', function () {
	return view('welcome');
});
```

Request type:

- get
- post
- put
- patch
- delete
- resource

Klasicke requesty (`GET`/`POST`) su bezproblemove, avsak `PUT`, `PATCH` a `DELETE` nemaju reprezentaciu v html. 

Treba pridat do formulara hidden input s nazvom `_method` s prislusnou hodnotou, alebo pouzivat zabudovany helper na to:

```php
{{ method_field('PUT') }}
``` 

*Aktualne cesty v aplikacii vieme ziskat pomocou prikazu*

```bash
php artisan route:list
```

**resource**: toto pouzivame v CRUD routingu, nakolko typ `resource` obsahuje zvysne typy

Priklad:

```
controller: SampleController

resource route obsahuje:

GET     /sample 
GET     /sample/create
POST    /sample
GET     /sample/{id}
PUT     /sample/{id}
GET     /sample/{id}/edit
DELETE  /sample/{id}
```

### controller

Umiestnenie: `project-root/app/Http/Controllers/`

#### Syntax

```php
class SampleController extends Controller
{
	public function index()
    {
    	// listing, route: /sample
	}

	public function create()
    {
    	// formular - vlozenie, route: /sample/create
	}

	public function store(Request $request)
    {
    	// ukladanie do DB, route: /sample
	}

	public function show($id)
    {
    	// detail, route: /sample/{$id}
	}

	public function edit($id)
    {
    	// formular na editaciu, route: /sample/{$id}/edit
	}

	public function update($id, Request $request)
    {
    	// ukladanie do DB po editacii, route: /sample/{$id}
	}

	public function show($id)
    {
    	// mazanie, route: /sample/{$id}
	}
}
```

*Generator:*

```bash
php artisan make:controller SampleController
```

### model

Umiestnenie: `project-root/app/`

#### Syntax

```php
class Sample extends Model
{
	protected $table = 'samples'; 			// nazov v DB 
    public $timestamps = true; 				// automaticke pridavanie timestamps

    protected $dates = ['deleted_at'];		// tzv. soft delete (nezmazeme, iba deaktivujeme)
    protected $fillable = [					// polia, ktore mozno naplnit datami od uzivatela
        'parent_id', 'name', 'description'
    ];
    protected $visible = [					// polia, ktore su zahrnute do selectov
        'parent_id', 'name', 'description'
    ];

    public function parent() { 				// tzv. Relationships v Eloquent. 
    	return $this->belongsTo(Parent::class);		// Zadefinujeme vztah medzi modelmi
    }

    public function child() {
    	return $this->hasMany(Child::class);		// 1 ** n
    }
}
```

##### Eloquent relationships:

- belongsTo 			parent
- belongsToMany 		n ** n
- hasOne 				1 ** 1
- hasMany				1 ** n

*Generator:*

```bash
php artisan make:model Sample
```

### eloquent

Databazova vrstva, mapuje DB na objekty.

#### Syntax

Request vrati `Eloquent kolekciu`.

Kazdy objekt ma svoje properties, na zaklade vztahov.

Napr. poznam id `Sample`, potrebujem najst `Parent`-a

```php
// 
$sample = Sample::find(1);

return $sample->parent;
```

### Migracie

```bash
php artisan make:migration create_samples_table
```

Vysledok:

```php
class CreateSamplesTable extends Migration
{
    public function up()
    {
        Schema::create(
            'samples',
            function (Blueprint $table) {
                $table->increments('id');
                $table->unsignedInteger('parent_id')->index();
                $table->string('name', 50)->default('Jozko Mrkvicka');
                $table->text('description')->nullable();
                $table->softDeletes();
                $table->timestamps();
            }
        );
    }

    public function down()
    {
        Schema::dropIfExists('samples');
    }
}
```

**Zapis migracii do DB**

```bash
php artisan migrate
```

- - - -

[Laravel CRUD app >](./crud.html)
