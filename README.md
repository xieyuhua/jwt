# jwt
jwt
Example
-------
```php
use jwt\JWT;
use jwt\Key;

$key = 'example_key';
$payload = [
    'iss' => 'http://example.org',
    'aud' => 'http://example.com',
    'iat' => 1356999524,
    'nbf' => 1357000000
];

$jwt = JWT::encode($payload, $key, 'HS256');
$decoded = JWT::decode($jwt, new Key($key, 'HS256'));
print_r($decoded);

$decoded = JWT::decode($jwt, new Key($key, 'HS256'),
$headers = new stdClass());
print_r($headers);
```


```php
use jwt\JWT;

$key = 'example_key';
$payload = [
    'iss' => 'http://example.org',
    'aud' => 'http://example.com',
    'iat' => 1356999524,
    'nbf' => 1357000000
];

$headers = [
    'x-forwarded-for' => 'www.google.com'
];

// Encode headers in the JWT string
$jwt = JWT::encode($payload, $key, 'HS256', null, $headers);

// Decode headers from the JWT string WITHOUT validation
// **IMPORTANT**: This operation is vulnerable to attacks, as the JWT has not yet been verified.
// These headers could be any value sent by an attacker.
list($headersB64, $payloadB64, $sig) = explode('.', $jwt);
$decoded = json_decode(base64_decode($headersB64), true);

print_r($decoded);
```
