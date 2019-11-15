# Custom Drush

Simple custom drush command in D8 using `hook_drush_command()` 

Unlike D7 .module is not required in module in D8. So we will only need `mymodule.info.yml` and `mymodule.drush.inc` .

 Where `mymodule.info.yml` defines the module and `mymodule.drush.inc` will implement `mymodule_drush_command()`

{% code title="mymodule.info.yml" %}
```yaml
name: mymodule
type: module
description: Simple custom drush cmd in d8
core: 8.x
```
{% endcode %}

{% code title="mymodule.drush.inc" %}
```php
/**
 * Implements hook_drush_command().
 *
 */
function mymodule_drush_command() {
    $commands = array();
    $commands['do-something'] = [
        'aliases' => ['ds'],
        'description' => 'Saying hello',
        'arguments' => [
          'args' => 'Arguments',
          ],
        'examples' => [
            'drush ds madan',
            'drush do-something madan',
         ]
     ];
    return $commands;
}

/**
 * Callback function for drush command.
 * The callback funciton has certain naming format.
 * drush_[MODULE_NAME]_[COMMAND_NAME]()
 *
 */
function drush_mymodule_do_something($arg = NULL) {
   $name = ['@arg' => $arg];
   drush_print('Hello, ' . $name);
}

```
{% endcode %}

