# Common

## String Interpolation (https://en.wikipedia.org/wiki/String_interpolation)

Bash
```bash
apples=4
echo "I have $apples apples"
# or
echo "I have ${apples} apples"
```

JavaScript (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
```javascript
const apples = 4;
const bananas = 3;
console.log(`I have ${apples} apples`);
console.log(`I have ${apples + bananas} fruit`);
```

PHP
```php
<?php
$apples = 5;
$bananas = 3;
echo "There are $apples apples and $bananas bananas.\n";
echo "I have ${apples} apples and ${bananas} bananas.";
```

Rust
```rust
let (apples, bananas) = (4, 3);
println!("There are {} apples and {} bananas.", apples, bananas);
```
## Query string

PHP
```php
$url = 'http://username:password@hostname:9090/path?arg=value#anchor';
parse_url($url, PHP_URL_QUERY)
// string(9) "arg=value"

$str = "first=value&arr[]=foo+bar&arr[]=baz";
// Recommended
parse_str($str, $output);
echo $output['first'];  // value
echo $output['arr'][0]; // foo bar
echo $output['arr'][1]; // baz

echo http_build_query([
    'foo' => 'bar',
    'baz' => 'boom',
    'cow' => 'milk',
    'php' => 'hypertext processor'
]);
// foo=bar&baz=boom&cow=milk&php=hypertext+processor
```

DOM
```javascript
const url = new URL('https://developer.mozilla.org/en-US/docs/Web/API/URL/search?q=123');
console.log(url.search);
// "?q=123"

let params;
params = new URLSearchParams(window.location.search);
params = (new URL('https://developer.mozilla.org/en-US/docs/Web/API/URL/search?q=123')).searchParams;
params.has('q');
// true
params.get('q');
// 123

```
