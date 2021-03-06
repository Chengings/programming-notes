# PHP

⭐️ [Clean Code PHP](https://github.com/jupeter/clean-code-php)

[PHP: The Right Way](https://phptherightway.com)

[Compact function](https://www.php.net/manual/en/function.compact.php).
Similar to [JavaScript's shorthand property names](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#New_notations_in_ECMAScript_2015)
```php
<?php
    $city  = "San Francisco";
    $state = "CA";
    $event = "SIGGRAPH";

    $location_vars = array("city", "state");

    $result = compact("event", $location_vars);
    print_r($result);
    /*
    Array
    (
        [event] => SIGGRAPH
        [city] => San Francisco
        [state] => CA
    )
    */
?>
```

[PHP 7.2 has new object type](https://www.php.net/manual/en/migration72.new-features.php)

[What does strict types do in PHP?](https://stackoverflow.com/a/48723830)

[Ignore vendor folder in PhpStrom](https://stackoverflow.com/a/38364125)

[Null coalescing operator - isset ternary](https://en.wikipedia.org/wiki/Null_coalescing_operator#PHP)
```php
$user = $this->getUser() ?? $this->createGuestUser();

/* Equivalent to */

$user = $this->getUser();

if (null === $user) {
    $user = $this->createGuestUser();
}
```
