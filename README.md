1. **How much data is sent in one run?**
    
    The publisher calls publish_event five times, sending five Borsh-serialized payloads around 24 bytes each, so 120 bytes total (excluding AMQP framing).
2. **Why do both publisher and subscriber use the same AMQP URL?**

    Both programs connect with amqp://guest:guest@localhost:5672 so they target the same RabbitMQ broker instance using identical credentials and network address. By sharing this URI, messages published by the publisher arrive at the exact broker and queue that the subscriber is listening on, enabling reliable communication between them.

- Running RabbitMQ as message broker
     ![alt text](img/img1.png)

- Sending and processing event
    ![alt text](img/img2.png)
    In the left terminal window we ran cargo run, which compiles the publisher and then sends five UserCreatedEventMessage events to RabbitMQ. In the right terminal window the subscriber was already listening on the same queue. As each event arrives, the handler prints lines showing that all five messages were received in real time.