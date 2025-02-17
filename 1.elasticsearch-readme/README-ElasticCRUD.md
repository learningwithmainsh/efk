# Elasticsearch CRUD Operations

This guide covers basic CRUD (Create, Read, Update, Delete) operations in Elasticsearch using RESTful API.

## Prerequisites
- Elasticsearch installed and running on `localhost:9200`
- cURL or a REST client like Postman

---

## 1. Create an Index
To create an index in Elasticsearch:
```sh
curl -X PUT "http://localhost:9200/my_index" -H 'Content-Type: application/json' -d'
{
  "settings": {
    "number_of_shards": 1,
    "number_of_replicas": 1
  }
}'
```

---

## 2. Insert a Document
To insert a document into an index:
```sh
curl -X POST "http://localhost:9200/my_index/_doc/1" -H 'Content-Type: application/json' -d'
{
  "name": "John Doe",
  "age": 30,
  "city": "New York"
}'
```

---

## 3. Retrieve a Document
To get a document by ID:
```sh
curl -X GET "http://localhost:9200/my_index/_doc/1"
```

---

## 4. Update a Document
To update an existing document:
```sh
curl -X POST "http://localhost:9200/my_index/_update/1" -H 'Content-Type: application/json' -d'
{
  "doc": {
    "age": 31
  }
}'
```

---

## 5. Delete a Document
To delete a document by ID:
```sh
curl -X DELETE "http://localhost:9200/my_index/_doc/1"
```

---

## 6. Delete an Index
To delete an index:
```sh
curl -X DELETE "http://localhost:9200/my_index"
```

---

## Additional Resources
- [Elasticsearch Documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html)

