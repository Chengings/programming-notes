# PHP

⭐️ [Clean Code PHP](https://github.com/jupeter/clean-code-php)

[PHP: The Right Way](https://phptherightway.com)

[Compact function](https://www.php.net/manual/en/function.compact.php)
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