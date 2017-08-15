# Controllers

- [Introduction](#introduction)
- [Basic Controllers](#basic-controllers)
    - [Defining Controllers](#defining-controllers)
- [Resource Controllers](#resource-controllers)
- [Dependency Injection & Controllers](#dependency-injection-and-controllers)

<a name="introduction"></a>
## Introduction

Instead of defining all of your request handling logic as Closures in route files, you may wish to organize this behavior using Controller classes. Controllers can group related request handling logic into a single class. Controllers are stored in the `app/Http/Controllers` directory.

<a name="basic-controllers"></a>
## Basic Controllers

<a name="defining-controllers"></a>
### Defining Controllers

Below is an example of a basic controller class.

    <?php

    namespace App\Http\Controllers;

    use App\User;
    use App\Http\Controllers\Controller;

    class UserController
    {
        /**
         * Show the profile for the given user.
         *
         * @param  int  $id
         * @return Response
         */
        public function show($id)
        {
            return view('user.profile', [
                'user' => User::findOrFail($id)
            ]);
        }
    }

You can define a route to this controller action like so:

    Route::get('user/{id}', 'UserController@show');

Now, when a request matches the specified route URI, the `show` method on the `UserController` class will be executed. Of course, the route parameters will also be passed to the method.

<a name="resource-controllers"></a>
## Resource Controllers

Laravel resource routing assigns the typical "CRUD" routes to a controller with a single line of code. For example, you may wish to create a controller that handles all HTTP requests for "photos" stored by your application. Using the `make:controller` Artisan command, we can quickly create such a controller:

    php artisan make:controller PhotoController --resource

This command will generate a controller at `app/Http/Controllers/PhotoController.php`. The controller will contain a method for each of the available resource operations.

Next, you may register a resourceful route to the controller:

    Route::resource('photos', 'PhotoController');

This single route declaration creates multiple routes to handle a variety of actions on the resource. The generated controller will already have methods stubbed for each of these actions, including notes informing you of the HTTP verbs and URIs they handle.

#### Actions Handled By Resource Controller

Verb      | URI                  | Action       | Route Name
----------|-----------------------|--------------|---------------------
GET       | `/photos`              | index        | photos.index
GET       | `/photos/create`       | create       | photos.create
POST      | `/photos`              | store        | photos.store
GET       | `/photos/{photo}`      | show         | photos.show
GET       | `/photos/{photo}/edit` | edit         | photos.edit
PUT/PATCH | `/photos/{photo}`      | update       | photos.update
DELETE    | `/photos/{photo}`      | destroy      | photos.destroy

#### Specifying The Resource Model

If you are using route model binding and would like the resource controller's methods to type-hint a model instance, you may use the `--model` option when generating the controller:

    php artisan make:controller PhotoController --resource --model=Photo

#### Spoofing Form Methods

Since HTML forms can't make `PUT`, `PATCH`, or `DELETE` requests, you will need to add a hidden `_method` field to spoof these HTTP verbs. The `method_field` helper can create this field for you:

    {{ method_field('PUT') }}


> Remember to keep your controllers focused. If you find yourself routinely needing methods outside of the typical set of resource actions, consider splitting your controller into two, smaller controllers.

<a name="dependency-injection-and-controllers"></a>
## Dependency Injection & Controllers

#### Method Injection

In addition to constructor injection, you may also type-hint dependencies on your controller's methods. A common use-case for method injection is injecting the `Illuminate\Http\Request` instance into your controller methods:

    <?php

    namespace App\Http\Controllers;

    use Illuminate\Http\Request;

    class UserController extends Controller
    {
        /**
         * Store a new user.
         *
         * @param  Request  $request
         * @return Response
         */
        public function store(Request $request)
        {
            $name = $request->name;

            //
        }
    }

If your controller method is also expecting input from a route parameter, simply list your route arguments after your other dependencies. For example, if your route is defined like so:

    Route::put('user/{id}', 'UserController@update');

You may still type-hint the `Illuminate\Http\Request` and access your `id` parameter by defining your controller method as follows:

    <?php

    namespace App\Http\Controllers;

    use Illuminate\Http\Request;

    class UserController extends Controller
    {
        /**
         * Update the given user.
         *
         * @param  Request  $request
         * @param  string  $id
         * @return Response
         */
        public function update(Request $request, $id)
        {
            //
        }
    }
