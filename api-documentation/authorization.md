# Authorization

Authorization is done via sending two headers:

1. **X-Processing-Key** – The public key, that can be obtained from user's account
2. **X-Processing-Signature** – POST body, signed by the secret key HMAC-SHA512, secret key is also obtained from user's account

See example below in PHP language

```php
$paramsArray = ['key' => 'value'];
$requestBody = json_encode($paramsArray);
$signature   = hash_hmac('sha512', $requestBody, $apiSecret);
```

Also, for all requests you need to use the next format key in the headers:

```php
"Content-Type": "application/json"
```

You can compare the validity of the signature that you generate with our example.

To do this the following data will be used:

```php
Secret key: AbCdEfG123456
Request body in JSON format:
{"currency":"BTC","foreign_id":"123456"}
```

With such data you should receive the following signature:

> 03c25fcf7cd35e7d995e402cd5d51edd72d48e1471e865907967809a0c189ba55b90815f20e2bb10f82c7a9e9d865546fda58989c2ae9e8e2ff7bc29195fa1ec

