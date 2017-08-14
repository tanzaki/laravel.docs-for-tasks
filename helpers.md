# Helpers

- [Introduction](#introduction)
- [Available Methods](#available-methods)

<a name="introduction"></a>
## Introduction

Laravel includes a variety of global "helper" PHP functions. Many of these functions are used by the framework itself; however, you are free to use them in your own applications if you find them convenient.

<a name="available-methods"></a>
## Available Methods

<style>
    .collection-method-list > p {
        column-count: 3; -moz-column-count: 3; -webkit-column-count: 3;
        column-gap: 2em; -moz-column-gap: 2em; -webkit-column-gap: 2em;
    }

    .collection-method-list a {
        display: block;
    }
</style>

[class_basename](#method-class-basename)
[snake_case](#method-snake-case)
[str_contains](#method-str-contains)
[str_plural](#method-str-plural)
[str_random](#method-str-random)
[str_singular](#method-str-singular)
[str_slug](#method-str-slug)
[title_case](#method-title-case)

</div>

### URLs

<div class="collection-method-list" markdown="1">

[route](#method-route)
[url](#method-url)

</div>

### Miscellaneous

<div class="collection-method-list" markdown="1">

[back](#method-back)
[csrf_field](#method-csrf-field)
[csrf_token](#method-csrf-token)
[dd](#method-dd)
[method_field](#method-method-field)
[redirect](#method-redirect)
[request](#method-request)
[view](#method-view)

</div>

<a name="method-listing"></a>
## Method Listing

<style>
    #collection-method code {
        font-size: 14px;
    }

    #collection-method:not(.first-collection-method) {
        margin-top: 50px;
    }
</style>

<a name="strings"></a>
## Strings

<a name="method-class-basename"></a>
#### `class_basename()` 

The `class_basename` returns the class name of the given class with the class' namespace removed:

    $class = class_basename('App\Foo\Bar\Comment');

    // Comment

<a name="method-snake-case"></a>
#### `snake_case()` 

The `snake_case` function converts the given string to `snake_case`:

    $snake = snake_case('fooBar');

    // foo_bar

    $snake = snake_case('Comment');

    // comment


<a name="method-str-plural"></a>
#### `str_plural()` 

The `str_plural` function converts a string to its plural form. This function currently only supports the English language:

    $plural = str_plural('comment');

    // comments

    $plural = str_plural('task');

    // tasks

    $plural = str_plural('child');

    // children

You may provide an integer as a second argument to the function to retrieve the singular or plural form of the string:

    $plural = str_plural('child', 2);

    // children

    $plural = str_plural('child', 1);

    // child

<a name="method-str-singular"></a>
#### `str_singular()` 

The `str_singular` function converts a string to its singular form. This function currently only supports the English language:

    $singular = str_singular('comments');

    // comment
    
<a name="method-str-slug"></a>
#### `str_slug()`

The `str_slug` function generates a URL friendly "slug" from the given string:

    $title = str_slug('Laravel 5 Framework', '-');

    // laravel-5-framework


<a name="method-title-case"></a>
#### `title_case()` 

The `title_case` function converts the given string to `Title Case`:

    $title = title_case('a nice title uses the correct case');

    // A Nice Title Uses The Correct Case

<a name="urls"></a>
## URLs

<a name="method-route"></a>
#### `route()` 

The `route` function generates a URL for the given named route:

    $url = route('routeName');

If the route accepts parameters, you may pass them as the second argument to the method:

    $url = route('routeName', ['id' => 1]);

By default, the `route` function generates an absolute URL. If you wish to generate a relative URL, you may pass `false` as the third parameter:

    $url = route('routeName', ['id' => 1], false);

<a name="method-url"></a>
#### `url()` 

The `url` function generates a fully qualified URL to the given path:

    echo url('user/profile');

    echo url('user/profile', [1]);

If no path is provided, a `Illuminate\Routing\UrlGenerator` instance is returned:

    echo url()->current();
    echo url()->full();
    echo url()->previous();

<a name="miscellaneous"></a>
## Miscellaneous

<a name="method-back"></a>
#### `back()` {#collection-method}

The `back()` function generates a redirect response to the user's previous location:

    return back();

<a name="method-csrf-field"></a>
#### `csrf_field()` {#collection-method}

The `csrf_field` function generates an HTML `hidden` input field containing the value of the CSRF token. For example, using [Blade syntax](/docs/{{version}}/blade):

    {{ csrf_field() }}

<a name="method-csrf-token"></a>
#### `csrf_token()` {#collection-method}

The `csrf_token` function retrieves the value of the current CSRF token:

    $token = csrf_token();

<a name="method-dd"></a>
#### `dd()` {#collection-method}

The `dd` function dumps the given variables and ends execution of the script:

    dd($value);

    dd($value1, $value2, $value3, ...);

If you do not want to halt the execution of your script, use the `dump` function instead:

    dump($value);

<a name="method-method-field"></a>
#### `method_field()` {#collection-method}

The `method_field` function generates an HTML `hidden` input field containing the spoofed value of the form's HTTP verb. For example, using [Blade syntax](/docs/{{version}}/blade):

    <form method="POST">
        {{ method_field('DELETE') }}
    </form>

<a name="method-redirect"></a>
#### `redirect()` {#collection-method}

The `redirect` function returns a redirect HTTP response, or returns the redirector instance if called with no arguments:

    return redirect('/home');

    return redirect()->route('route.name');

<a name="method-request"></a>
#### `request()` 

The `request` function returns the current [request](/docs/{{version}}/requests) instance or obtains an input item:

    $request = request();

    $value = request('key', $default = null)

<a name="method-view"></a>
#### `view()` {#collection-method}

The `view` function retrieves a [view](/docs/{{version}}/views) instance:

    return view('auth.login');
