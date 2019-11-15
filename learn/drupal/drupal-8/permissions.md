# Permissions

In Drupal 8 the `hook_permission()` to create permission has been replaced by `module.permissions.yml` file. 

#### Static Permission

{% code title="mymodule.permissions.yml" %}
```yaml
my custom permission:
    title: 'My custom module permission'
    description: 'This is a custom module permission'
    restrict access: TRUE
```
{% endcode %}

#### Dynamic Permission

Sometimes we might require to create a permission during runtime as it might depend on something else.

 Example: _node_ module defines a set of permissions for each node bundle defined by modules. However, they can not be set statically as the type of node bundles will change. This is where setting permission dynamically comes in handy. 

We can define a callback in `.permissions.yml` file which will return a list of dynamic permissions.

{% code title="mymodule.permissions.yml" %}
```yaml
permission_callbacks:
    - Drupal\mymodule\MyModulePermissions::permissions
```
{% endcode %}

{% code title="mymodule/MyModulePermissions.php" %}
```php
class MyModulePermissions {
    public function permissions() {
        $permissions = [];
        
        //create our array list of permissions
        $permissions['mypermissionname'] = [
            'title' => 'title of my permission',
            'description' => 'Something something'
        ];
        
        return $permissions;
    }
}
```
{% endcode %}

