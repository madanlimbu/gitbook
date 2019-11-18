# Graph Databases

### Intro

GD are NoSQL Database. Stores Data based on Graph Concepts \( Vertex, Edges, Properties\). Relationship are first class Entities \( Can store properties in relationship \).

Useful on multi relationship scenario \( Solves complexity of multi relation / Indirect relation traversing in Relational Database \). Flexible for continuously changing Data. Efficiently navigate through connected data.

#### Nodes \( Vertices \)

* \(Labels\) Type 
* Properties \( Key = "Value" Pairs \)
* Doesn't force schema \( Properties of 2 Different Node of Same Label / Type doesn't need to have same properties \)

#### Relationship \( Edges \)

* Type \( Type of relationship \) 
* Properties
* Connects Nodes
* Has Direction \( Bi-Directional, Uni-Directional, Direction it faces \)

### Graph Data Models

#### RDF \(Resource description framework\)

Vertices \(Resources: URIs & Attribute values: Literal Values\) & Edges \( Relationships: URIs \)

Works with subject - predicate - object, Example: `Jon drops tear` where Jon = Subject, Drops = Predicate & Tear = Object 

Subject \( Resource or Node \) , Predicate \( Edge \) & Object \( Node or literal Value \) in Graph.

Uses triplestore to store data.  Uses URI to identify Nodes & Edges \( No internal structure like Property model \). Entities are triples. No unique instances of  relationship of same type.

Efficient to find relationship in data  or unknown information from the data.

Data can be from multi sources & we can detach the schema from the data then apply our own schema or interlink data to create relationship between data objects.

Create Rules, Set Facts which creates Inferred Facts. 

```text
Example:
Rules:
    - Animal under same type class are family.
    - Mammal is a type class.
Facts:
    - Cat is Mammal
    - Dog is Mammal
Inferred Facts:
    - Cat & Dog (Subject/Object) are family (Predicate).
```



#### Labelled \(Property Model\)

Uses Nodes, Edges & Properties \( Key Value Pairs \) with both Nodes & Edges having Type & Unique ID. Both Nodes & Edges are first class hence Separate Entities for Node & Edges with properties.

Efficient in traversing relationship in data.

From above example, Cat & Dog node will need to have `is_a_family` relationship/edges between them during creation or we will have to traverse through Cat & Dog having `under_same_type_class` relationship/edges to find the relationship. 

![](https://www.ontotext.com/wp-content/uploads/2019/10/Database-comparison-infographicFinal.svg)



