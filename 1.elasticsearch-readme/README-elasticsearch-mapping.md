# Elasticsearch Mapping Guide

## Overview
Mapping in Elasticsearch defines how documents and their fields are stored and indexed. It is equivalent to defining a schema in traditional databases. Elasticsearch supports two types of mapping:

1. **Dynamic Mapping** - Fields are automatically detected and mapped.
2. **Explicit Mapping** - Fields and their data types are defined manually.

## 1. Dynamic Mapping
By default, Elasticsearch enables dynamic mapping, which means new fields in a document will be automatically added to the index with an inferred type.

### Example:
```json
PUT my_index/_doc/1
{
  "name": "John Doe",
  "age": 30,
  "email": "john.doe@example.com"
}
```
In this case, Elasticsearch will automatically map:
- `name` as `text`
- `age` as `long`
- `email` as `text`

### Disabling Dynamic Mapping:
You can disable dynamic mapping by setting `dynamic: false`.
```json
PUT my_index
{
  "mappings": {
    "dynamic": false
  }
}
```

## 2. Explicit Mapping
Explicit mapping allows defining field types and settings manually, ensuring better control over the data structure.

### Example:
```json
PUT my_index
{
  "mappings": {
    "properties": {
      "name": { "type": "text" },
      "age": { "type": "integer" },
      "email": { "type": "keyword" },
      "created_at": { "type": "date" }
    }
  }
}
```

### Benefits of Explicit Mapping:
- Ensures correct data types.
- Allows customization (e.g., setting an analyzer for text fields).
- Prevents unexpected changes in data types.

## Updating Mapping
Elasticsearch does **not** allow modifying existing field types directly. Instead, you need to create a new index and reindex the data.

## Conclusion
Understanding mapping is crucial for optimizing search performance and ensuring data consistency. While dynamic mapping is useful for flexibility, explicit mapping provides greater control and efficiency.

For more details, refer to the [Elasticsearch official documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping.html).

