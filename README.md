# Consume Messages from DLQ
## Step-1: Fix the error which caused records to land into DLQ
There are many reasons (serde errors, bad data, schema errors) which lands records into DLQ. Read more about this here: https://www.confluent.io/blog/kafka-connect-deep-dive-error-handling-dead-letter-queues/

So the first step is to check the error stack which will be available in record's header and fix the error. Confluent users can check the header in UI as explained here: https://docs.confluent.io/cloud/current/connectors/dead-letter-queue.html

## Step-2: Consume Records

> DONOT add the dlq topic into same connector. It will create an infinite loop.

In Kafka, DLQ is also another topic. Create a new connector with source as the 'DLQ topic' and sink it to the same system. As the cause of error was fixed in step-1, this time the records should get into Sink system without any issues

## Screenshots
I used S3 Sink connector
![consume-dlq-messages](https://user-images.githubusercontent.com/73946498/183341968-b9a32bae-277d-4879-8ddc-227fc858c551.png)
