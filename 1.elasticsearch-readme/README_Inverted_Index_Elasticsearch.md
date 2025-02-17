# Inverted Index with Elasticsearch

## Overview
This project demonstrates how to create and query an **Inverted Index** using **Elasticsearch**. An inverted index is a fundamental data structure used in search engines to map content keywords to their locations in documents.

## Prerequisites
- **Elasticsearch** (v7.x or later)
- **Kibana** (optional, for visual interaction)
- **cURL** or any API testing tool (like Postman)
- Basic knowledge of REST APIs

## Setup Instructions

### 1. Install Elasticsearch
Download and install Elasticsearch from the [official website](https://www.elastic.co/downloads/elasticsearch) or use Docker:

```bash
docker pull elasticsearch:7.17.0
docker run -d --name elasticsearch -p 9200:9200 -e "discovery.type=single-node" elasticsearch:7.17.0
```

### 2. Verify Installation
Check if Elasticsearch is running:

```bash
curl -X GET "localhost:9200/"
```

You should receive a JSON response with cluster details.

## Creating an Inverted Index

### 1. Create an Index
Create an index called `documents`:

```bash
curl -X PUT "localhost:9200/documents" -H 'Content-Type: application/json' -d'
{
  "settings": {
    "number_of_shards": 1,
    "number_of_replicas": 0
  },
  "mappings": {
    "properties": {
      "title": { "type": "text" },
      "content": { "type": "text" }
    }
  }
}'
```

### 2. Index Documents
Add some sample documents to the index:

```bash
curl -X POST "localhost:9200/documents/_doc/1" -H 'Content-Type: application/json' -d'
{
  "title": "Elasticsearch Basics",
  "content": "Elasticsearch is a powerful search engine based on Lucene."
}'

curl -X POST "localhost:9200/documents/_doc/2" -H 'Content-Type: application/json' -d'
{
  "title": "Introduction to Inverted Index",
  "content": "An inverted index maps keywords to document locations."
}'

curl -X POST "localhost:9200/documents/_doc/3" -H 'Content-Type: application/json' -d'
{
  "title": "Advanced Elasticsearch",
  "content": "Learn advanced features of Elasticsearch and how inverted indexes improve performance."
}'
```

### 3. Search Documents
Search for documents containing the keyword "Elasticsearch":

```bash
curl -X GET "localhost:9200/documents/_search" -H 'Content-Type: application/json' -d'
{
  "query": {
    "match": {
      "content": "Elasticsearch"
    }
  }
}'
```

### 4. View Inverted Index (Term Vectors)
To see how Elasticsearch tokenizes and indexes your content, use the term vectors API:

```bash
curl -X GET "localhost:9200/documents/_termvectors/1" -H 'Content-Type: application/json' -d'
{
  "fields": ["content"]
}'
```

## Explanation of Inverted Index
An inverted index in Elasticsearch works by:
1. **Tokenizing** the text into individual terms.
2. **Storing** a list of documents for each term.
3. **Querying** efficiently by matching terms to document IDs.

For example, if you search for "Elasticsearch," the inverted index quickly retrieves all document IDs where the term exists.

## Troubleshooting
- Ensure Elasticsearch is running on port 9200.
- Check for JSON syntax errors in your API requests.
- Use Kibana's Dev Tools for easier query testing.

## Conclusion
By following this guide, you've set up an inverted index in Elasticsearch, indexed documents, and performed search queries. This setup forms the foundation of powerful full-text search capabilities.

## References
- [Elasticsearch Official Documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html)
- [Inverted Index Explanation](https://en.wikipedia.org/wiki/Inverted_index)

---
Feel free to contribute to this project by opening issues or submitting pull requests!

