# Tutorial 8
Farrel Ayman Abisatyo  <br>
2206828916 <br>
Advanced Programming B <br>

## Reflection
### 1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?
- Unary: a type of communication protocol that allows client-server interactions 
where the client sends a single request to the server and gets a single response back. Suitable when you want to fetch a single item from a database, authenticate a user, or perform a calculation and obtain the result
- Server streaming: communication protocol that allows the server to send a stream of responses to the client. This pattern is suitable in scenarios where the server needs to push a large amount of data or a continuous stream of updates to the client.
- Bi-directional: The client and server can send multiple messages to each other in a continuous stream. Suitable in scenarios where there is a need for ongoing, interactive communication.

### 2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?
- Authentication <br>
  Secure your gRPC service by using mutual Transport Layer Security (TLS). This requires both the client and server to verify each other's identity through certificates to ensure that communication occurs between trusted parties.
- Authorization <br>
Once authentication is established, implement access control to restrict who can access specific resources. This can be achieved through Role-Based Access Control (RBAC), where permissions are granted based on user roles, 
or Attribute-Based Access Control (ABAC), where access is granted based on attributes such as user attributes or request context.
- Data Encryption <br>
To protect data confidentiality, ensure that sensitive data is encrypted both when stored (at rest) and during transmission (in transit). For data in transit, use TLS to secure the communication channel, preventing unauthorized access to the data being exchanged.

### 3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?
Most likely issues that amy arise are concurrency issues, connection management, and security/authentication. There are of course mitigations that we
can apply to each of these issues:
- using Arc, Mutex, or RwLock to manage concurrency resources
- Implementing robust connection handling for connection management
- using TLS to secure streams to unsure that only authorized clients can connect and communicate.

### 4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?
Advantages
- It works seamlessly with Tokio, a widely-used asynchronous runtime in the Rust ecosystem.
- With ReceiverStream, you can easily create asynchronous and concurrent gRPC services, allowing for parallel processing of multiple streams.

Disadvantages
- It is a bit complex to understand for developers who arent familiar with asynchronous programming.
- Managing errors in asynchronous streams can be complex, with multiple points where things can go wrong.

### 5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?
I believe we can achieve this by adhering to the design principles we've learned in class, for example:
- Apply modular design to our application architecture to encapsulate specific functionalities.
- Establish clear interfaces for communication between different modules.
- Design our gRPC services with extensibility in mind to accommodate future.

### 6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?
MyPaymentService implementation might require additional steps to ensure secure, reliable, and accurate handling of payments.
These goals may be achieved by a few approaches:
- implementing mechanisms to authenticate clients, such as JWT, or other token-based approaches.
- check for required fields and correct data types.
- Use Transport Layer Security (TLS) for secure data transmission. Encrypt sensitive payment information.

### 7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?
I believe that adoption of gRPC as a communication protocol provides high-performance, cross-platform communication, and improving security and observability. 
However, it can present challenges in terms of learning curve and also interoperability with non-gRPC systems.

### 8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?
HTTP/2 offers significant advantages over HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs because it has a lot to offer in terms of performance, efficiency, and features like multiplexing 
and server push. However, it can also cause increase complexity and require additional considerations for debugging and monitoring. 

### 9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?
Rest API is lightweight and easy-to-use. Consequently it works well for simple interactions, but because of its send and wait nature, is not ideal for real-time updates 
communication. Meanwhile gRPC, with its bidirectional streaming, can provide a robust solution for real-time and responsive communication, 
allowing clients and servers to send and receive messages continuously.

### 10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?
The implication of using protobuf is that it requires Protobuf requires defining a clear schema in .proto files, ensuring that the structure of messages and data types is consistent. Consequently,
even though it has more complexity, it ensures type safety reducing the risk of runtime errors. Meanwhile, JSON's flexible structure makes it easier for developers to experiment, work quickly, and also read easily.
However by not defining a clear schema, it lacks strict type enforcement and can lead to issues with data validation.