# Custom block

#### Custom block intro

Custom block in D7 is registered using  [`hook_block_info()`](https://api.drupal.org/api/drupal/modules%21block%21block.api.php/function/hook_block_info/7.x) ,  However , it is very memory inefficient as Drupal has to read and store whole `.module` files in memory at runtime. 

#### Custom block example

```php
/**
 * Implements hook_block_info().
 */
function hello_block_info() {
  $blocks = array();
  $blocks['hello_block'] = array(
    'info' => t('Hello block')
  );
```



