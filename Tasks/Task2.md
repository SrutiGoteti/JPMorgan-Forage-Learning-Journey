# Task 2 - Kafka Listener Integration

## Objective

Integrate Apache Kafka into Midas Core by implementing a Kafka Listener that consumes incoming transaction messages from the configured Kafka topic.

## Background

Midas Core receives transaction requests through Kafka rather than directly from a frontend application.

Using Kafka introduces an additional messaging layer between producers and consumers, providing several architectural advantages:

* Decoupling of frontend and backend services
* Asynchronous message processing
* Improved fault tolerance
* Horizontal scalability through multiple producers and consumers

In this task, Midas Core acts as a Kafka consumer that listens for incoming transaction messages.

## Technologies Introduced

* Apache Kafka
* Spring Kafka
* Kafka Producers
* Kafka Consumers
* Kafka Listener
* Message Serialization
* Message Deserialization

## Architecture

```text
Transaction Producer
        ↓
Kafka Topic (trader-updates)
        ↓
Kafka Listener
        ↓
Transaction Object
```

The producer publishes transaction messages to Kafka, while Midas Core consumes and deserializes those messages into Java Transaction objects.

## Implementation Plan

### Step 1: Create Kafka Listener

Create a Spring Component that acts as a Kafka consumer.

Responsibilities:

* Subscribe to the configured Kafka topic
* Receive incoming messages
* Deserialize messages into Transaction objects

### Step 2: Configure Topic Subscription

Use the Kafka topic configured in application.yml:

```yaml
general:
  kafka-topic: trader-updates
```

This allows the listener to remain configurable without hardcoding the topic name.

### Step 3: Implement Message Handler

Implement a listener method using Spring Kafka's `@KafkaListener` annotation.

The listener should:

* Receive Transaction objects
* Allow Spring Kafka to perform automatic deserialization
* Perform no business logic at this stage

### Step 4: Verify Kafka Integration

Run:

```bash
mvn -Dtest=TaskTwoTests test
```

The embedded Kafka instance supplied by the test framework automatically starts and injects itself into the Spring application context.

### Step 5: Debug Incoming Transactions

Set a breakpoint inside the Kafka listener method.

Run TaskTwoTests in Debug mode.

Inspect the first four received Transaction objects and record:

* Amount 1
* Amount 2
* Amount 3
* Amount 4

### Step 6: Submit Results

Submit the four transaction amounts observed during debugging.


