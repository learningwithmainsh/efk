# Elasticsearch Indices

This document provides an overview of the Elasticsearch indices used in this project, including their structure, settings, and usage.

## Table of Contents
1. [Introduction](#introduction)
2. [Indices Overview](#indices-overview)
3. [Index Settings and Mappings](#index-settings-and-mappings)
4. [Index Management](#index-management)
5. [Query Examples](#query-examples)
6. [Best Practices](#best-practices)
7. [References](#references)

## Introduction
Elasticsearch is a distributed, RESTful search and analytics engine capable of solving a growing number of use cases. This project leverages Elasticsearch for efficient searching, indexing, and analysis of data.

## Indices Overview
Below are the primary indices used in this project:

| Index Name       | Description                       | Primary Fields             |
|------------------|-----------------------------------|-----------------------------|
| `users_index`    | Stores user information           | `user_id`, `name`, `email` |
| `logs_index`     | Stores system logs                | `timestamp`, `level`, `message` |
| `products_index` | Stores product details            | `product_id`, `name`, `price`, `category` |
| `orders_index`   | Stores order information          | `order_id`, `user_id`, `total`, `status` |

## Index Settings and Mappings
Each index is configured with specific settings and mappings to optimize performance and search accuracy.

### Example Settings for `users_index`
```json
{
  "settings": {
    "number_of_shards": 3,
    "number_of_replicas": 2
  },
  "mappings": {
    "properties": {
      "user_id": { "type": "keyword" },
      "name": { "type": "text" },
      "email": { "type": "keyword" },
      "created_at": { "type": "date" }
    }
  }
}
```

## Index Management

### Creating an Index
```bash
curl -X PUT "localhost:9200/users_index" -H 'Content-Type: application/json' -d @settings.json
```

### Deleting an Index
```bash
curl -X DELETE "localhost:9200/users_index"
```

### Updating Index Settings
```bash
curl -X PUT "localhost:9200/users_index/_settings" -H 'Content-Type: application/json' -d '{
  "index" : {
    "number_of_replicas" : 1
  }
}'
```

## Query Examples

### Basic Search Query
```json
{
  "query": {
    "match": {
      "name": "John Doe"
    }
  }
}
```

### Filtering by Date Range
```json
{
  "query": {
    "range": {
      "created_at": {
        "gte": "2023-01-01",
        "lte": "2023-12-31"
      }
    }
  }
}
```

## Best Practices
- Use `keyword` type for exact matches and `text` type for full-text search.
- Optimize shard and replica settings based on your cluster size and query load.
- Regularly monitor index performance using Elasticsearch's built-in tools.
- Implement proper index lifecycle management (ILM) to automate index rollover and deletion.

## References
- [Elasticsearch Documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html)
- [Index Settings](https://www.elastic.co/guide/en/elasticsearch/reference/current/index-modules.html)
- [Query DSL](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html)

---

Feel free to contribute by opening issues or submitting pull requests!

