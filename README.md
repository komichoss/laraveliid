# komicho\laraveliid
Build a separate disambiguation for specific categories (IID) . [wikipedia](https://en.wikipedia.org/wiki/IID_(disambiguation))

## use
```php
use Komicho\Laravel\Traits\LaravelIid;
```

---

## functions
### createiid
```php
Model::createiid($data);
```

---

## variables
### $guideColumn
```php
protected static $guideColumn = '<column_name>';
```
Type the name of the column through which the group sequence is selected.

## database > migrations
### add column
You must add this column.
```php
...

$table->integer('iid')->nullable();

...
```

## Full example:-
Specify a sequence for each project.
### Model :-
```php
<?php

use Komicho\Laravel\Traits\LaravelIid;

class Backlog extends Model
{
    use LaravelIid;

    protected static $guideColumn = 'project_id';
    
    ...
}
```
### Controller :-
```php
<?php

namespace App\Http\Controllers;

use App\Backlog;

use Illuminate\Http\Request;

class BacklogController extends Controller
{

    ...

    public function store(Request $request)
    {
        Backlog::createiid($request->all());
        return back();
    }

    ...

}
```