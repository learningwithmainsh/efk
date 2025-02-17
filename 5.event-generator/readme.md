
# EFK Stack Setup and Logs

## Steps to Set Up

1. Navigate to the `efk-stack/event-generator` directory:

   ```bash
   cd efk-stack/event-generator
   ```

2. Apply the Fluent Bit configuration:

   ```bash
   kubectl apply -f webapp-fluent-bit.yaml
   kubectl get pods -n efk
   kubectl logs -f app-event-simulator -n efk
   ```

3. Apply the configurations and check the pods:

   ```bash
   kubectl apply -f .
   kubectl get pod -n efk
   ```

4. Navigate to the directory for index management:

   ```bash
   /app/management/data/index_management/indices
   ```

## Exploring and Analyzing Ecommerce Logs with the EFK Stack

In these labs, you will set up and validate a Fluent Bit logging solution in a Kubernetes environment with Elasticsearch, Fluentd, and Kibana (EFK) already installed. The labs include both multiple-choice questions and hands-on tasks to help you understand and work with EFK.

### Initial Setup:

- **Verify Cluster Configuration**: Ensure you can access the Kubernetes cluster and that it is configured correctly for the EFK stack.

### Deployment:

- **Apply Configurations**: Deploy the event generator and Fluent Bit configurations using the `kubectl apply -f .` command from the cloned repository.

### Kibana Configuration:

- **Access Kibana**: Open the Kibana UI and set up index management to view logs.

### Verification:

- **Check Log Streaming**: Ensure Fluent Bit is streaming logs from the event generator pod to Kibana.

### Validation Tasks:

- **Index Pattern Verification**: Verify that the data view for the specified index pattern exists and is correctly set up in Kibana.

---

## Question 1: Setting Up the Environment

### Objective: Ensure the student is able to interact with the Kubernetes cluster and access Elasticsearch.

- **Access the Kubernetes Cluster**: Use kubectl commands to verify access to the Kubernetes cluster.
  
  Run:

  ```bash
  kubectl get nodes
  ```

  Ensure the cluster is up and running.

- **Get the ClusterIP of Elasticsearch Service**: Run:

  ```bash
  kubectl get svc -n efk
  ```

  Get the ClusterIP of the Elasticsearch service.

- **Verify Elasticsearch Access**: Use `curl` to check the health of the Elasticsearch cluster.

  Run:

  ```bash
  kubectl get svc elasticsearch -n efk -o jsonpath='{.spec.clusterIP}' | xargs -I {} curl -X GET "http://{}:9200/_cluster/health?pretty"
  ```

---

### Task: Deploy the event generator to generate logs for testing

Navigate to `/root/efk-stack/event-generator`.

---

## Exploring and Analyzing Ecommerce Logs with the EFK Stack

### Create a Data View in Kibana

1. Access the Kibana UI and navigate to Index Management.
2. Locate the index named `logstash-yyyy.dd.mm` under the Indices section.
3. Create a data view with the following specifications:
   - **Name**: kubesystem
   - **Index Pattern**: logstash-yyyy.dd.mm
4. Save the data view and verify that it appears in the Discover tab.

---

### Verify Log Streaming

#### Task: Confirm that logs are being properly streamed and indexed.

1. **Visit Kibana Dashboard and Verify Indexes**:
   - Open Kibana in your web browser.
   - Navigate to the Index Management section under Stack Management.
   - Look for the Index named `logstash-yyyy.mm.dd`.
   - Click on the index name to ensure it is available and has data.

2. **Run KQL Queries to Search for Specific Log Data**:
   - Go to the Discover section in Kibana.
   - Select the index pattern corresponding to the `logstash-yyyy.mm.dd` index.
   - In the search bar, enter the desired Kibana Query Language (KQL) query to search for logs.

---

### Answer the Following Question

Which KQL query should you use to find all logs related to users who encountered failed logins or other issues with the app?

