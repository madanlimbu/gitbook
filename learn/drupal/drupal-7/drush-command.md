# Custom Drush Command

Simple Drush command using `hook_drush_command()` .

```php
/**
 * hook_drush_command().
 *
 */
function mymodule_drush_command() {
    $items = array();
    $items['something'] = array(
        'aliases' => array('go'),
        'description' => 'Something about drush cmd',
        'callback' => 'do_something',
    );
    return $items;
}

/**
 * Call back function when drush cmd is executed.
 *
 */
function do_something() {
    drush_print('hello');
}
```

