# Kafka Order Streaming Demo

This project is a simple hands-on implementation of an **event streaming pipeline using Apache Kafka**.
The goal of this project was to understand how producers, brokers, and consumers interact in a real streaming system.

Instead of building a complex application, this project focuses on the **core Kafka workflow**: sending events to a topic and consuming them in real time.

---

## What This Project Does

The system simulates a **food order streaming system**.

1. A **Python producer** generates an order event.
2. The order is sent to a **Kafka topic (`orders`)**.
3. A **Python consumer** subscribes to the topic.
4. The consumer reads the order event and prints the processed order.

This demonstrates how **event-driven systems process data asynchronously**.

Example order event:

```json
{
  "order_id": "uuid",
  "user": "nicole",
  "item": "mushroom burger",
  "quantity": 10
}
```

---

## Tech Stack

* Apache Kafka
* Docker & Docker Compose
* Python
* confluent-kafka Python client

---

## Architecture

Producer → Kafka Broker → Consumer

* **Producer** publishes order events
* **Kafka** stores events inside topics
* **Consumer** reads and processes events

---

## Kafka Setup

Kafka runs inside Docker using **KRaft mode** (Kafka without Zookeeper).

Key configurations used:

* Single node Kafka cluster
* Controller + Broker in same container
* Topic replication factor = 1
* Port exposed: `9092`

This allows local development without running a full distributed Kafka cluster.

---

## Producer

The producer:

* Generates a unique order ID using `uuid`
* Converts order data to JSON
* Sends the message to the `orders` topic
* Uses a callback to confirm message delivery

Key learning points:

* Kafka messages are **byte data**
* JSON serialization is needed for structured data
* Delivery callbacks confirm successful publishing

---

## Consumer

The consumer:

* Subscribes to the `orders` topic
* Continuously polls Kafka for new messages
* Decodes JSON messages
* Processes and prints the order

Example output:

```
Received order: 10 x mushroom burger from nicole
```

Key learning points:

* Consumers read messages using **polling**
* Kafka consumers belong to **consumer groups**
* Offset management controls message reading

---

## How to Run

### 1. Start Kafka with Docker

```bash
docker compose up -d
```

### 2. Install dependencies

```bash
pip install confluent-kafka
```

### 3. Run Producer

```bash
python producer.py
```

### 4. Run Consumer

```bash
python consumer.py
```

---

## What I Learned

Through this project I understood:

* How **Apache Kafka works as a distributed event streaming platform**
* The difference between **producers and consumers**
* How **Kafka topics store streaming data**
* How **consumer groups enable scalable message processing**
* How to run Kafka locally using **Docker and KRaft mode**
* How Python applications interact with Kafka using the **confluent-kafka client**

---

## Future Improvements

Some things I plan to explore next:

* Multiple partitions and consumer scaling
* Kafka message keys and ordering
* Schema management using Avro / Schema Registry
* Integrating Kafka with real applications or microservices

---

## Why I Built This

I built this project to understand **real-time data pipelines and event-driven architecture**, which are widely used in modern systems like payment processing, analytics pipelines, and microservices communication.

This project helped me move from **theoretical understanding of Kafka to a working implementation**.
