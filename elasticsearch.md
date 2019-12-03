# Exact match querying

    $ curl -XGET "http://yourserver:9200/entities/track/_search" -H 'Content-Type: application/json' -d' 
    {
      "query": {
        "term": {
          "<field>.keyword": {
            "value": "<exact value>"
          }
        }
      }
    }'

This will eliminate results that contain <exact value> but are not strictly <exact value>.
