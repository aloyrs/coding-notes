1. Install PHP using XAMPP
2. Install COMPOSE (PHP dependecy manager)
3. Run below to create a laravel app named example-app

```php
composer create-project laravel/laravel example-app
```

4.

```php
cd example-app
```

# Connect to DB

```php
// Can now run laravel web app using
php artisan serve
```

To connect to mySQL database:
I use mySQL workbench
Connect a connection
Create a database eg.

![alt text](image.png)

Add database details to .env file

![alt text](image-1.png)

# Create model migration

```php
php artisan make:model ListItem -m

// This creates a ListItem model (/app/Models)

// and a migration file (/database/migrations) where I can configure the table columns which will be created
```

```php
php artisan migrate

//Migrate meaning create tables in connected database
```

Now my database looks like this , because there are multiple default tables

![alt text](image-3.png)

![alt text](image-2.png)

# Example (Create list Item , add to DB)

```php
// welcome.blade.php file

<body>
  <h1>To do list</h1>

  <form method="POST" action="/list-items" accept-charset="UTF-8">
    @csrf
    <label for="listItem">New todo Item</label>
    <input type="text" name="listItem" required />
    <button type="submit">Add Item</button>
  </form>
</body>
```

```php
//web.php

Route::post('/list-items', [TodoListController::class, 'store']);
```

```php
//TodoListController.php

class TodoListController extends Controller
{
    public function store(Request $request)
    {
        $request->validate([
            'listItem' => 'required|string|max:255',
        ]);

        $listItem = new ListItem();
        $listItem->name = $request->input('listItem');
        $listItem->is_complete = 0; // Default to not completed
        $listItem->save();

        return redirect()->back()->with('success', 'Item added successfully!');
    }
}

```
