Drupal relation note
====================

Module reference
----------------
* https://drupal.org/project/relation

All code examples originated from relation module.

Relation API
------------
### Create relation type
    $relation_type = array(
      'relation_type' => 'directional_entitydifferent',
      'label' => 'directional_entitydifferent',
      'directional' => TRUE,
      'source_bundles' => array('user:*'),
      'target_bundles' => array('node:page'),
    );
    relation_type_save($relation_type);

### Save a relation
    $relation = relation_create($relation_type, $endpoints);
    $rid = relation_save($relation);

### Delete a relation
    relation_delete($relation_id);

### Relation query
Get relations for node 1 (symmetric, directional, octopus), limit to directional and octopus with relation_type().

    $relations = relation_query('node', $this->node1->nid)
      ->propertyCondition('relation_type', array(
        $this->relation_types['directional']['relation_type'],
        $this->relation_types['octopus']['relation_type'],
      ))
      ->execute();

Get last two relations for node 1.

    $relations = relation_query('node', $this->node1->nid)
      ->range(1, 2)
      ->propertyOrderBy('rid', 'ASC')
      ->execute();


Relation type settings
----------------------
除了relation_type, 其餘都是非必要欄位

* relation_type: Relation type machine name (string).
* label: defaults to relation_type.
* directional: 預設false.
* transitive: 預設false.
* r_unique: 設定relation是否可重複,預設false
* min_arity: 預設2
* max_arity: 預設2
* source_bundles: 設定關係來源，格式為'entity:bundle'，設定'entity:*'表示屬於指定entity type的所有bundle皆可為source_bundle.
* target_bundles: 設定關係目標，directional設定為true時才有作用

