# Entity

### Node

The `node` table holds the basic information about the node, the `nid` is the primary key on this table and contains the `vid` field which is a foreign key to the `node_revision` table. The `node_revision` table holds each revision of the node, the `vid` is the primary key on this table and contains the `nid` field which is a foreign key to `node` table.

The `node` table only contains one record relating to a node and also stores the current `vid` whereas the `node_revision` table contains the revision data.

All `field` tables have 2 versions, `field_data_[field_name]` and `field_revision_[field_name]`, the data tables contain the current revision and the revisions table contain the revision data.

