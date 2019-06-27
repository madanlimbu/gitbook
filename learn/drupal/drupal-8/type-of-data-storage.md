---
description: >-
  In this section we will go through type of data storage system in D8 and when
  to use them with examples and snippets.
---

# Data system

### State

Simple key/value pool, can store values of any type as they will be serialised and unserialised automatically. 

Used to store information about the current system's state. 

Stored in database and not meant to be exported between environment like configuration.  

Note: Best practice to namespace state entry `key` names with module name, ie. "`mymodule.last_person_name`".

```text
#get a value
$val = \Drupal::state()->get('key');

#get multiple key/value pairs:
$pairs = \Drupal::state()->getMultiple($keys);

#set a value
\Drupal::state()->set('key', 'value');

#set multiple values
\Drupal::state()->setMultiple($key_values);

#delete a value
\Drupal::state()->delete('key');
```

{% embed url="https://www.drupal.org/docs/8/api/state-api/overview" %}

{% embed url="https://api.drupal.org/api/drupal/namespace/Drupal%21Core%21KeyValueStore/8.2.x" %}

Note: **State API** uses the **Key/Value Store API** under the hood. The keys are name-spaced to a "_collection_" and the State API is simply one of the collection. 

### Content / Entities

Entity API has 3 layers:

1. **Entity Types** define different business logic for different objects. _Examples: Nodes, Users, Taxonomy Terms, Comments and Custom Blocks_
2. **Entity Bundles** are different configurations of the same Entity Type, with different Field configuration. _Examples: page nodes, article nodes and event nodes \(bundles of "`node`" Entity Type\)_
3. **Fields** are basic unit of Drupal content/entity. A field is a single rich-value _\( not "string" or "int" but value like "email-address", "formatted text", or "telephone number" \). It can also be a reference to another entity._

_We  can think entity as a collection of field, and all Field types has capability to be translated to make content multi-lingual._

{% embed url="https://www.drupal.org/docs/8/api/entity-api/creating-a-content-entity-type-in-drupal-8" %}

### Configuration

Used to store, manage and deploy administrator-provided configuration.

Configuration system is modelled as a key-value store \( note it doesn't use Key/Value Store API\). Keys are dot-delimited strings, and the values are specifically "Configuration objects".

Config objects have get\(\) and set\(\) methods to manage properties on the object. Config objects can be safely serialised to YAML and unserialised from YAML. 

There is also "_**Configuration Entities**_" which provides **CRUD** behaviour using the basic Entity API but backed by the `Configuration API`. Configuration Entities do not have Fields but uses mostly the same API. They are most useful when we need multiple instances of a given configuration object \(Also the storage mechanism under most Plugins\). Examples: View

{% embed url="https://www.drupal.org/docs/8/api/configuration-api/creating-a-configuration-entity-type-in-drupal-8" %}

{% embed url="https://www.drupal.org/docs/8/api/configuration-api/simple-configuration-api" %}

### Tempstore

Two tempstores types: `private` and `shared`

Used when data need to be persisted between requests without being saved back in storage. It works similar to session. 

Main difference between **session** and tempstores\(**shared**\) is tempstores\(**shared**\) is shared between users, whereas **session** aren't.

Both **tempstores** uses Key/Value API internally and uses its variant called "`expirable`" where values will get cleared out eventually. 

Examples: ****

**private-tempstores** are usually used when building complex multi-step UIs, 

 **shared-tempstores** are used in Views \(configuration entity\) - Even without saving, every time a setting field is changed a temp copy of view config entity is saved to shared tempstore. After changing all the fields config and saving, the temporary copy is written back to config system and temp version is cleared. 

## Tips on which data storage system to use:

* if it is being _deployed to different environmen_t use **Configuration system**
* if being _deployed  on different environment_ and could be _arbitrary number_ of them use **Config Entities**
* _user-generated_ content use **Content Entity**
* _large unstructured_ data need to be looked up by _ID_ and _cannot_ be _deployed_ use  **Key/Value Store**
* if _session-like temporary_ storage use **tempstore**
* if used to be in _variables table \(d7\)_ or _current system states_ which _cannot be deployed_ use State

## Snippets:

#### Sessions

Getting session variables and setting session variables

```text
$session = \Drupal::request()->getSession();
$session->set('name', 'madan');
$session->get('name');
```

