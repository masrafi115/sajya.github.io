---
title: HTTP JSON-RPC Client
description: HTTP JSON-RPC Client for Laravel
extends: _layouts.documentation
section: content
---


The HTTP(S) Client is a standalone package that uses your PHP code to make requests. Built on [Laravel](https://laravel.com/docs/8.x/http-client#introduction) (Doesn't require the entire framework, just its component) expressive HTTP shell, it allows you to customize things like authorization, retries, and more.


## Install

Go to the project directory and run the command:

```php
$ composer require sajya/client
```


## Usage

```php
use Illuminate\Support\Facades\Http;
use Sajya\Client\Client;

// Create the JSON RPC client
$client = new Client(Http::baseUrl('http://localhost:8000/api/v1/endpoint'));

// Call the 'tennis' method on the server
$response = $client->execute('tennis@ping');

// Print the response from the server
$response->result(); // pong
```

By default, the request identifier will be generated using the [UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier), you can get it by calling the `id()` method

```php
$response->id();
```

To get the result of an error, you need to call the `error()` method

```php
$response->error();
```

### Parameters

Example with positional parameters:

```php
$response = $client->execute('tennis@ping', [3, 5]);
```

Example with named arguments:

```php
$response = $client->execute('tennis@ping', ['end' => 10, 'start' => 1]);
```

### Batch requests

Call several procedures in a single HTTP request:

```php
$responses = $client->batch(function (Client $client) {
    $client->execute('tennis@ping');
    $client->execute('tennis@ping');
});
```

### Notify requests

```php
$client->notify('procedure@method');
```
