---
description: Examples of D7 to D8/9/10 migration
---

# Migration

## Source plugin

#### Custom source plugin (D7 Group entity to D8 +)

```php
// Example a custom module (group_migrate)
// File dir on module - src/Plugin/migrate/source
<?php

namespace Drupal\group_migrate\Plugin\migrate\source;

use Drupal\Core\Extension\ModuleHandlerInterface;
use Drupal\migrate\Row;
use Drupal\migrate_drupal\Plugin\migrate\source\d7\FieldableEntity;
use Drupal\Core\Entity\EntityTypeManagerInterface;
use Drupal\Core\State\StateInterface;
use Drupal\migrate\Plugin\MigrationInterface;
use Symfony\Component\DependencyInjection\ContainerInterface;

/**
 * Source plugin to get generic D7 group data.
 *
 * @code
 * source:
 *   plugin: d7_group
 *   group_type: page
 * @endcode
 *
 *
 * @code
 * source:
 *   plugin: d7_group
 *   group_type: [page, test]
 * @endcode
 *
 *
 * For additional configuration keys, refer to the parent classes.
 *
 * @see \Drupal\migrate\Plugin\migrate\source\SqlBase
 * @see \Drupal\migrate\Plugin\migrate\source\SourcePluginBase
 *
 * @MigrateSource(
 *   id = "d7_group",
 *   source_module = "rct_migrate"
 * )
 */
class D7GroupEntity extends FieldableEntity {
  /**
   * The module handler.
   *
   * @var \Drupal\Core\Extension\ModuleHandlerInterface
   */
  protected $moduleHandler;

  /**
   * {@inheritdoc}
   */
  public function __construct(array $configuration, $plugin_id, $plugin_definition, MigrationInterface $migration, StateInterface $state, EntityTypeManagerInterface $entity_type_manager, ModuleHandlerInterface $module_handler) {
    parent::__construct($configuration, $plugin_id, $plugin_definition, $migration, $state, $entity_type_manager);
    $this->moduleHandler = $module_handler;
  }

  /**
   * {@inheritdoc}
   */
  public static function create(ContainerInterface $container, array $configuration, $plugin_id, $plugin_definition, MigrationInterface $migration = NULL) {
    return new static(
      $configuration,
      $plugin_id,
      $plugin_definition,
      $migration,
      $container->get('state'),
      $container->get('entity_type.manager'),
      $container->get('module_handler')
    );
  }

  /**
   * {@inheritdoc}
   */
  public function query() {
    $query = $this->select('groups', 'g')
      ->fields('g', [
        'gid',
        'type',
        'title',
      ]);

    if (isset($this->configuration['group_type'])) {
      $query->condition('g.type', (array) $this->configuration['group_type'], 'IN');
    }

    return $query;
  }

  /**
   * {@inheritdoc}
   */
  public function prepareRow(Row $row) {
    $gid = $row->getSourceProperty('gid');
    $type = $row->getSourceProperty('type');

    // Get Field API field values.
    foreach ($this->getFields('group', $type) as $field_name => $field) {
      $row->setSourceProperty($field_name, $this->getFieldValues('group', $field_name, $gid));
    }

    // If the group title was replaced by a real field using the Drupal 7 Title
    // module, use the field value instead of the group title.
    if ($this->moduleExists('title')) {
      $title_field = $row->getSourceProperty('title_field');
      if (isset($title_field[0]['value'])) {
        $row->setSourceProperty('title', $title_field[0]['value']);
      }
    }

    return parent::prepareRow($row);
  }

  /**
   * {@inheritdoc}
   */
  public function fields() {
    $fields = [
      'gid' => $this->t('Group ID'),
      'type' => $this->t('Type'),
      'title' => $this->t('Title'),
    ];
    return $fields;
  }

  /**
   * {@inheritdoc}
   */
  public function getIds() {
    $ids['gid']['type'] = 'integer';
    $ids['gid']['alias'] = 'g';
    return $ids;
  }
}

```

```yaml
# Using source plugin
# Migrating D7 group entity to D8+ group entity
id: group_migrate_test
source:
  plugin: d7_group
  group_type: d7_test_group
process:
  label:
    - plugin: get
      source: title
destination:
  plugin: entity:group
  bundle: d9_test_group
```
