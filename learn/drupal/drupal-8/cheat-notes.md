# Cheat Notes

#### D8 Modules Structures:

* module in `.info.yml`
* routes in `.routing.yml`
* link to menu system in `.menu.yml`
* css/JS libraries in `.libraries.yml`
* permissions `.permissions.yml`

#### Useful function of php module in Drupal

`php_eval` which is a wrapper around php eval function. 

Can be useful when wanting to run a function from drush. 

```text
drush php_eval "echo drupal_get_installed_schema_version('modulename');"
drush php_eval "echo drupal_set_installed_schema_version('modulename', '8000');"
```



