---
description: Quick helpful notes on Elastic-search
---

# Elasticsearch

#### Intro

Uses [Apache Lucene](https://lucene.apache.org/) search engine in core. [JSON Based Query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html), Schema-less & Distributed (Shards) .

Can use aggregations alongside search requests ( we can search documents, filter results, and perform aggregations on that search context ).

* **Document**: Collection of fields in the key-value pairs containing our data
* **Indexed:** Document stored (Optimised collection of documents)
* **Shards:** Divided indices (data) into different nodes(servers) of a cluster for horizontal scaling&#x20;
* **Relevance score**: how well each document matches a query (default sorting)

#### Basic **Elasticsearch** communication

```
curl -X<HTTP_METHOD> '<PROTOCOL>://<HOST>:<PORT>/<PATH>?<QUERY_STRING>' -d '<BODY>'

#HTTP_METHOD: GET, POST, PUT, HEAD, DELETE
#PROTOCOL: http/https
#PORT: Default ES Http service (9200)
#PATH: API Endpoint  "index_name/_doc/unique_document_id" "index_name/_search"
#QUERY_STRING: optional strings 
#BODY: JSON-encoded request body
```

#### [Bulk API](https://www.elastic.co/guide/en/elasticsearch/reference/7.6/docs-bulk.html) can be used to perform bulk indexing or delete operations.

```
#bulk operation to index bulk_data.json 
curl -H "Content-Type: application/json" -XPOST "localhost:9200/index_name/_bulk?pretty&refresh" --data-binary "@bulk_data.json"

#lists the indices status & docs.count 
curl "localhost:9200/_cat/indices?v"
```

#### Searching&#x20;

We can do search by requesting on `_search` endpoint. The results are structured in following way:

```
{
    hits: {
        total: {
            value: 100 #total number result found
        },
        hits: [ #array of results docs (10 by default)
            { 
                key: value #data inside doc
                _score: value #documents relevance score
            },
            {
                key: value
                _score: value #documents relevance score
            }
        ]
    }
}
```

There is no state in Elasticsearch between searches, however for usage like pagination we can use `from` & `size` parameters to get results from hits.&#x20;

_**Note**: hits starts from `0`_&#x20;

#### [Query DSL](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html) (Domain Specific Language)

```
#Two types of caluses:

#1) Leaf (looks for particular value in particular field)
match, should, must_not, term, range

#2) Compound (combines with leaf or compound)
bool, dis_max, filter
```

Relevance score (`_score`) will also depend on which context query clause is running on.

Query context: Check if document matches & how relevant the document is ( `_score` ).

Filter context: Absolute answer&#x20;

### Inverted index

How the data is structure/stored for fast search.

![Inverted index example](../../.gitbook/assets/screenshot-2020-07-01-at-7.03.19-pm.png)

### String

In ES string can be saved as **Text** or **Keyword**.&#x20;

Difference being **Text** type will tokenize / normalize before saving to inverted index. However, Keyword would directly add it to inverted index.

_Example: "hello world", In **Text** would be added as ("hello", "world") but as "hello world" in **Keyword**._

## Term and Match Query&#x20;

Term query looks for exact match of Search (String) but In Match query Search  (String) are analysed before look up.

{% embed url="https://www.youtube.com/watch?v=nShb3MWYppI" %}

{% embed url="https://www.youtube.com/watch?v=oPObRc8tHgQ" %}



&#x20;

