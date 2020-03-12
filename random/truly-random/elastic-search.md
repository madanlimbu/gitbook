---
description: Quick helpful notes on Elastic-search
---

# Elasticsearch

#### Intro

Uses [Apache Lucene](https://lucene.apache.org/) search engine in core. [JSON Based Query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html), Schema-less & Distributed \(Shards\) .

Can use aggregations alongside search requests \( we can search documents, filter results, and perform aggregations on that search context \).

* **Document**: Collection of fields in the key-value pairs containing our data
* **Indexed:** Document stored \(Optimised collection of documents\)
* **Shards:** Divided indices \(data\) into different nodes\(servers\) of a cluster for horizontal scaling 
* **Relevance score**: how well each document matches a query \(default sorting\)

#### Basic **Elasticsearch** communication

```text
curl -X<HTTP_METHOD> '<PROTOCOL>://<HOST>:<PORT>/<PATH>?<QUERY_STRING>' -d '<BODY>'

#HTTP_METHOD: GET, POST, PUT, HEAD, DELETE
#PROTOCOL: http/https
#PORT: Default ES Http service (9200)
#PATH: API Endpoint  "index_name/_doc/unique_document_id" "index_name/_search"
#QUERY_STRING: optional strings 
#BODY: JSON-encoded request body
```

#### [Bulk API](https://www.elastic.co/guide/en/elasticsearch/reference/7.6/docs-bulk.html) can be used to perform bulk indexing or delete operations.

```text
#bulk operation to index bulk_data.json 
curl -H "Content-Type: application/json" -XPOST "localhost:9200/index_name/_bulk?pretty&refresh" --data-binary "@bulk_data.json"

#lists the indices status & docs.count 
curl "localhost:9200/_cat/indices?v"
```

#### Searching 

We can do search by requesting on `_search` endpoint. The results are structured in following way:

```text
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

There is no state in Elasticsearch between searches, however for usage like pagination we can use `from` & `size` parameters to get results from hits. 

_**Note**: hits starts from `0`_ 

#### [Query DSL](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html) \(Domain Specific Language\)

```text
#Two types of caluses:

#1) Leaf (looks for particular value in particular field)
match, should, must_not, term, range

#2) Compound (combines with leaf or compound)
bool, dis_max, filter
```

Relevance score \(`_score`\) will also depend on which context query clause is running on.

Query context: Check if document matches & how relevant the document is \( `_score` \).

Filter context: Absolute answer 

