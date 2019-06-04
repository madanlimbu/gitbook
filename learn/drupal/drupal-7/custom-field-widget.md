# Custom Field Widget

## Drupal 7 – Creating Custom Field Widget for Term Reference Field Type

I Recently, I had to override the auto complete widget of Drupal 7 Taxonomy Term reference to give the result in a way that is different to default format. Here is how I accomplished this task.

### **Simple Steps :** 

1.  Register Widget by calling `hook_field_widget_info`
2. Register a callback URL for Autocomplete using `hook_menu`
3. Create a Form and register our URL in `autocomplete_path` using `hook_field_widget_form`
4. Create our autocomplete function that gives Result in a way we want

### **Register Widget**

```php

/**
* Altered Copy of taxonomy_field_widget_info.
*
*/
function our_module_field_widget_info() {
    return array(
        'our_module_autocomplete_widget' => array(
        'label' => t('Name of widget'),
        'field types' => array(
            #Taxonomy Feidl Type
            'taxonomy_term_reference'
        ),
        'settings' => array(
            'size' => 60,
            'autocomplete_path' => 'our_module_url_path/autocomplete',
        ),
        'behaviors' => array(
            'multiple values' => FIELD_BEHAVIOR_CUSTOM,
        ),
        ),
    );
}
```

### **Register Callback**

```php
/**
* Implements hook_menu.
* Copy of taxonomy_menu
* Altered page callback method to our own custom method
*
*/
function our_module_menu() {
    $items = array();
    $items['our_module_url_path/autocomplete'] = array(
        'title' => 'Autocomplete Taxonomy',
        'page callback' => 'our_module_autocomplete_callback',
        'access arguments' => array(
            'access content',
        ),
        'type' => MENU_CALLBACK
    );
    retrun $items;
}
```

### **Create Form and Register our URl**

Implement same method as `taxonomy_field_widget_form` from taxnomy module in our module.

Change the `#autocomplete_path` to the URL path we create in our hook\_menu path.

### **Create Custom Autocomplete Function** 

Create a function that handles the URL path we created earlier and set the function name in `hook_menu` callback.

Can copy `taxonomy_autocomplete` method and override it with feature we want our call back to answer.

