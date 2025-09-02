# Web API Essentials: REST API and GraphQL

Notes on Module2 of the Coursera - Application Development using Microservices and Serverless

---

## API Gateways

---

### What is an API Gateway?

- API Management Tool
- Sits between client and collection of backend services
- It aggregates the various services required to fulfill them and returns the appropriate result.

### Why do you use API Gateway?

- Protect your APIs from malicious usage or overuse. Thus you can use authentication service with rate limiting.
- Analyze your API usage using analytics and monitoring services.
- Monetize your APIs by using billing system.
- A Gateway also presents a single point of contact to your various microservices and provides a single response to a request.
- Finally, you can seamlessly remove or add APIs without the client's knowledge about the services running at backend.

### Gateway to microservices

#### Let's say a online store follows microservice architecture. Some of services will be

- Product Information Service
- Inventory Service
- Order Service
- Authentication Service etc.

#### How does the client access the microservices?

- This is a problem when you need to interact with multiple APIs.

#### API Gateway can resolve the problem

- You can change hosts and location of endpoints without impacting the client.
- Services can be scaled up or down
- Services can be replaced.

### Benefits of Using API Gateway

- Insulate the client from how the app is partitioned into microservices. It simplifies the client side by moving the logic of calling multiple services from the client to the API Gateway.
- It also provides optimal APIs for each client, regardless of who the client is.
- It reduces the number of requests or round trips. For example, instead of making separate calls to the Product Information Service, Inventory Service, and Order Service, the client can make a single call to the API Gateway, which then aggregates the responses from the various services.
- Irrespective of how your microservices communicate internally, an API Gateway will provide a standard protocol to communicate with outside world.

### Drawbacks of using API Gateway

- It is another component, that needs to be developed and maintained.
- If not designed carefully, it can become a bottleneck and a single point of failure.
- It will increase response time, due to additional network step in the execution of application.

### API Gateway Products

#### Managed Gateways

- IBM DataPower Gateway
- Google Apigee / Cloud Endpoints
- Microsoft Azure API Gateway
- AWS API Gateway

#### Open Source Gateways

- Kong Gateway
- Apache APISIX
- Tyk (This also has a managed version)
- Gloo (This is also available as an enterprise version)

---

## cURL

---

- `cURL` short for "Client URL"
- Command line tool that enables data transfer over various network protocol.
- Used in command line or scripts to transfer data.
- Most common use cases
  - Downloading file from internet
  - Endpoint Testing
  - Debugging
  - Error Logging
- Protocols Supported by `cURL` are
  - HTTP
  - HTTPS
  - FTP
  - IMAP

### Common cURL Commands

| Command | Description                                                                         |
| ------- | ----------------------------------------------------------------------------------- |
| `-X`    | Specifies the request method to use (GET, POST, PUT, DELETE, etc.)                  |
| `-H`    | Specifies the headers to include in the request (e.g., Content-Type, Authorization) |
| `-d`    | Specifies the data to include in the request body (for POST and PUT requests)       |

---

## Basics of GraphQL

---

### What is GraphQL?

- Query language for your API.
- Allows clients to Fetch (only) what's needed.
- Can be developed using any programming language, since it is _language agnostic_.

### Fetch (only) what's needed

- Avoids over-fetching
- Avoids under-fetching
- Requires one endpoint to retrieve all necessary data

### REST vs GraphQL

| REST                                                                                                     | GraphQL                                                                      |
| -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| APIs are the **resources** that provide endpoints to perform a particular operation using an HTTP method | Type you define in the schema are the nodes. Here API is treated as a graph. |
| You make multiple calls, and receive whatever is sent by the server                                      | You only request and receive what you require.                               |
| Supports API Versioning                                                                                  | No API Versioning                                                            |

### GraphQL Terms

- `Query` used for querying your data, more like a get request
- `Fields` are the specific data points you want to retrieve from your API.
- `Mutations` are used to modify server-side data, more like post/put/delete requests.
