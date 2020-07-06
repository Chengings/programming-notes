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
