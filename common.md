# Common

📚
 * ⭐️ https://www.programming-idioms.org/
 * Go & Node.js https://github.com/miguelmota/golang-for-nodejs-developers

## String Interpolation https://en.wikipedia.org/wiki/String_interpolation

Bash
```bash
apples=4
echo "I have $apples apples"
# or
echo "I have ${apples} apples"
```

JavaScript https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
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

## Character
https://en.wikipedia.org/wiki/Regular_expression#Character_classes
| POSIX      | ASCII         | VIM  |
| ---------- | ------------- | ---- |
| [:digit:]  | [0-9]         | \d   |
| [:xdigit:] | [A-Fa-f0-9]   | \x   |
| [:lower:]  | [a-z]         | \l   |
| [:upper:]  | [A-Z]         | \u   |
| [:alpha:]  | [A-Za-z]      | \a   |
| [:alnum:]  | [A-Za-z0-9]   |      |
| [:blank:]  | [ \t]         | \s   |
| [:space:]  | [ \t\r\n\v\f] | \\_s |

https://en.wikipedia.org/wiki/Glob_(programming)#Compared_to_regular_expressions
| glob | regular expression |
| ---- | ------------------ |
| ?    | .
| *    | .*

## Null coalescing operator https://en.wikipedia.org/wiki/Null_coalescing_operator
Bash
```bash
#suppliedTitle='supplied title'
title=${suppliedTitle:-'Default title'}
echo "$title" # prints: Default title
```

JavaScript
```javascript
const title = suppliedTitle ?? 'Default title'; // null or undefined
const title = suppliedTitle || 'Default title'; // Any falsy value: null, undefined, "", 0, NaN, false
```

PHP
```php
$title = $suppliedTitle ?? 'Default title';
// strictly for NULL or a non-existent variable/array index/property. In this respect, it acts similarly to isset() 
```

Python
```python
title = suppliedTitle or "Default title"
42    or "something"  # returns 42
0     or "something"  # returns "something"
None  or "something"  # returns "something"
False or "something"  # returns "something"
""    or "something"  # returns "something"
```
