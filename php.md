# PHP

📚
 * Request for Comments (RFC) https://wiki.php.net/rfc

---

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

## PHP 8

__Constructor Property Promotion__ https://wiki.php.net/rfc/constructor_promotion

PHP < 8
```php
class Point {
    public float $x;
    public float $y;
    public float $z;
 
    public function __construct(
        float $x = 0.0,
        float $y = 0.0,
        float $z = 0.0,
    ) {
        $this->x = $x;
        $this->y = $y;
        $this->z = $z;
    }
}
```

PHP ≥ 8
```php
class Point {
    public function __construct(
        public float $x = 0.0,
        public float $y = 0.0,
        public float $z = 0.0,
    ) {}
}
```

__Match expression v2__ https://wiki.php.net/rfc/match_expression_v2

PHP < 8
```php
switch ($this->lexer->lookahead['type']) {
    case Lexer::T_SELECT:
        $statement = $this->SelectStatement();
        break;
 
    case Lexer::T_UPDATE:
        $statement = $this->UpdateStatement();
        break;
 
    case Lexer::T_DELETE:
        $statement = $this->DeleteStatement();
        break;
 
    default:
        $this->syntaxError('SELECT, UPDATE or DELETE');
        break;
}
```

PHP ≥ 8
```php
$statement = match ($this->lexer->lookahead['type']) {
    Lexer::T_SELECT => $this->SelectStatement(),
    Lexer::T_UPDATE => $this->UpdateStatement(),
    Lexer::T_DELETE => $this->DeleteStatement(),
    default => $this->syntaxError('SELECT, UPDATE or DELETE'),
};
```

__Nullsafe operator__ https://wiki.php.net/rfc/nullsafe_operator

PHP < 8
```php
$country =  null;
 
if ($session !== null) {
    $user = $session->user;
 
    if ($user !== null) {
        $address = $user->getAddress();
 
        if ($address !== null) {
            $country = $address->country;
        }
    }
}
```

PHP ≥ 8
```php
$country = $session?->user?->getAddress()?->country;
```
