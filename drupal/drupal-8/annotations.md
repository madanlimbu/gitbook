# Annotations

#### Annotations intro

In Drupal 8 annotations are used for class discovery and metadata description. They are written as PHP comments above a class or function.

Annotations are read and parsed at runtime by an annotation engine which turns it into an object which PHP can use.

Annotations are mostly used to register a class as a plugins. 

#### Example of Block plugin using annotation

```php
/**
 * Provides a 'Hello' Block
 *
 * @Block(
 *   id = "hello",
 *   admin_label = "Hello block",
 * )
 */
```

Block manager search for file containing @Block annotation tag and makes it available to a region. `id` is the machine name and `admin_label` is how it will appear in UI.

> Note: We can use `getinfo()` method inside plugins class instead of annotation but it uses more memory.

#### General rules for Annotations

Following are general rules on Annotations:

* Translatable string wrapped in `@Translation(`\) 
* strings - double quotes
* lists - curly brackets
* maps - curly brackets and equality for key-value 
* booleans - TRUE/FALSE \(no quotes\)
* numbers - \(no quotes\)

#### References:

[BeFused - Intro to Annotations](https://befused.com/drupal/annotations)

