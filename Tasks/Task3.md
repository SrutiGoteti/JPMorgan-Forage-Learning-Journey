# Task 3 - Database Integration and Transaction Persistence

## Objective

Integrate Midas Core with an H2 in-memory database and persist valid transactions received through Kafka.

The system must:

* Validate incoming transactions
* Update sender and recipient balances
* Store valid transactions in the database
* Discard invalid transactions

---

## Background

Until Task 2, Midas Core could receive transaction messages from Kafka but did not store them.

Task 3 introduces a database layer using H2 and Spring Data JPA. Since financial data requires reliability and consistency, transactions are validated before being recorded.

A transaction is valid only if:

* The sender exists
* The recipient exists
* The sender has sufficient balance

When valid:

* Sender balance is decreased
* Recipient balance is increased
* Transaction is stored in the database

When invalid:

* No database changes are made

---

## Technologies Introduced

* H2 In-Memory Database
* Spring Data JPA
* Hibernate ORM
* JPA Entities
* JPA Relationships (`@ManyToOne`)
* Kafka Consumer Integration

---

## Implementation Steps

### Step 1: Create TransactionRecord Entity

Create a new JPA entity:

```text
TransactionRecord.java
```

Purpose:

* Represents transactions stored in the database
* Separate from the `Transaction` DTO received from Kafka

---

### Step 2: Define Entity Relationships

Add relationships between transactions and users:

```java
@ManyToOne
private UserRecord sender;

@ManyToOne
private UserRecord recipient;
```

This allows:

* One user to send many transactions
* One user to receive many transactions

---

### Step 3: Create TransactionRepository

Create:

```text
TransactionRepository.java
```

Extending:

```java
CrudRepository<TransactionRecord, Long>
```

Purpose:

* Save transaction records
* Access stored transactions

---

### Step 4: Update Kafka Listener

Modify:

```text
KafkaTransactionListener.java
```

to:

* Receive transactions
* Validate sender and recipient
* Check available balance
* Process valid transactions

---

### Step 5: Update User Balances

For valid transactions:

```text
Sender Balance = Sender Balance - Amount

Recipient Balance = Recipient Balance + Amount
```

Save updated users using `UserRepository`.

---

### Step 6: Persist Transaction Records

Create a new `TransactionRecord` object and save it using:

```java
transactionRepository.save(...)
```

---

### Step 7: Ignore Invalid Transactions

If validation fails:

* Do not update balances
* Do not store transaction records

---

### Step 8: Run TaskThreeTests

Run:

```bash
mvn -Dtest=TaskThreeTests test
```

or debug `TaskThreeTests`.

---

### Step 9: Find Waldorf's Balance

Using the debugger:

1. Let all transactions process.
2. Inspect the database or user records.
3. Find the user named **waldorf**.
4. Record the final balance.
5. Round it down to the nearest integer.
6. Submit the value as the Task 3 answer.

