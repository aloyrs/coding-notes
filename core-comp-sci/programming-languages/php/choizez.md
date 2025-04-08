After working with from July 2024,
I learnt that a PHP Laravel app uses a MVC architecture

# Laravel Flow: Blade View, Route, and Controller

1. Blade view template (frontend html)

```php
 <form action="{{ route('user.store') }}" method="POST">
```

2. Route File , route from frontend(view) to backend(controller)

```php
    Route::post('/user/store', [UserController::class,'store'])->name('user.store');
```

3. Route File , route from frontend(view) to backend(controller)

```php
    public function store(Request $request){

    $user = User::create($request->all());
    return redirect()->route('user.index')->with('success', 'User created successfully!');
}
```
