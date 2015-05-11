ElasticSearch HTTP API
======================

Brief how-to API calls. In the following examples replace `localhost` with 
your ip or hostname.

| Description                               | API call                                                                  |
|-------------------------------------------|---------------------------------------------------------------------------|
| Get list of indices verbose               |`http://localhost:9200/_cat/indices?v`                                     | 
| Get entries from an index (collection)    |`http://localhost:9200/{INDEX_NAME}/_search?pretty=true&q=*:*&size=100`    |
| Get index (collection) statistics         |`http://localhost:9200/{INDEX_NAME}/_stats`                                |