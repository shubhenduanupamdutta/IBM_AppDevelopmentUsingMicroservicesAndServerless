# Serverless Overview

---

## Introduction to Serverless Computing

---

Cloud Native Computing Foundation (CNCF) defines `serverless` as:

_The concept of building and running applications that do not require server management._

_It describes a finer-grained deployment model where applications bundled as one or more functions, are uploaded to a platform and then executed and scaled, and billed in response to the exact demand needed at the moment._

In other words, serverless computing allows developers to focus on writing code without worrying about the underlying infrastructure. The cloud provider manages the servers, scaling, and maintenance, allowing for rapid development and deployment of applications.

### Serverless = FaaS + BaaS

Think of serverless as a combination of two main components:

1. **Function as a Service (FaaS)**: This is where developers write individual functions that are executed in response to events. These functions are stateless and can be triggered by various events such as HTTP requests, database changes, or file uploads. Examples of FaaS platforms include AWS Lambda, Google Cloud Functions, and Azure Functions.
2. **Backend as a Service (BaaS)**: This refers to third-party services that provide backend functionality, such as databases, authentication, and storage. Developers can leverage these services without having to manage the underlying infrastructure. Examples of BaaS providers include Firebase, Auth0, and AWS Amplify.

### Evolution to Serverless Computing

Progress from traditional to serverless leads to

- Faster Deployment
- Shorter Lifespans
- Increased Productivity

Several milestones mark this evolutionary trend:

- **Physical Machines**: Hampered by upfront investments, capacity planning, and more. Physical machines take weeks and months to deploy and have a lifespan of several years.
- **Virtualization/Cloud Computing**: Virtualization technology is implemented in cloud computing for faster provisioning, high scalability and availability. Virtualization facilitates creation of multiple virtual machines (VMs) or containers. And VMs take minutes to deploy and have a lifespan of days or weeks.
- **Containers**: Containers are lightweight, portable, and provide a consistent environment for applications. Containers take seconds to deploy and have a lifespan of hours or days.
- **Serverless**: Require only serverless architecture for the core code. Serverless functions take milliseconds to deploy and have a lifespan of seconds or minutes.

### Serverless Architecture Concepts

- Abstracts infrastructure and software environment
- Code runs in a cloud platform
- Cloud provider manages the hardware and software setup, security, performance, scaling and so on.
- Billed only for usage.
- Developer only need to focus on code and business logic in the form of functions.

### Serverless Characteristics

- **Hostless**: No need to manage servers or infrastructure.
- **Elastic**: Automatically scales up or down based on demand.
- **Load Balanced**: Distributes incoming requests across multiple instances.
- **Stateless**: Each function invocation is independent and does not retain state between executions.
- **Event-driven**: Functions are triggered by events such as HTTP requests, database changes, or file uploads.
- **High Availability**: Built-in redundancy and failover mechanisms to ensure uptime. with no extra effort or cost.
- **Usage-based Billing**: Pay only for the compute time and resources consumed during function execution.

### Developer's Role

Focus on application development:

- Build functions using popular programming languages.
- Extend functionality
- Perform better testing, since functions only perform one task at a time.
- Optimize apps and functions
- Improve user experience

### Cloud Provider Responsibilities

Cloud provider manage common infrastructure and maintenance tasks such as:

- Maximizing Utilization
- Minimizing Costs
- Server Management (OS Updates and Security Patches)
- Auto-scaling
- High Availability
- Security
- Performance (low latency)
- Monitoring and Logging

---

## Serverless Pros and Cons

---

- In traditional computing, development and operations team set up and maintain infrastructure, middleware, and runtime environments.
- Setup and deployments are time consuming, complex and expensive.
- Arrival of cloud, containers, and serverless computing means developers can focus on writing code and business logic.
- Developers can build and run apps in milliseconds, without worrying about infrastructure, scalability or fault tolerance.
- Challenges include vendor lock-in, cold starts, and debugging difficulties, 3rd party dependencies, and networking.

### Serverless Computing Benefits

- **Reduced Cost**: There are no infrastructure setup and maintenance requirements because cloud provider manages it, thereby reducing operational costs. Pay only for what you use.
- **Built-in HA and FT**: Cloud performs maintain reliability thereby maintaining high availability and fault tolerance.
- **Increased dev productivity**: Developers can focus on writing code and business logic, leading to faster development cycles and quicker time-to-market.
- **Code runs when triggered**: Functions are executed in response to events, allowing for efficient resource utilization.
- **Fast run times**: Functions run in milliseconds, enabling rapid execution of tasks. Where as VMs and containers take anywhere from seconds to minutes to start up.
- **Built-in Code Editor**: Many cloud providers offer a web-based code editor for writing and testing functions, for faster development.
- **Pay as you go**: Billing is based on actual usage, with no upfront costs or long-term commitments.
- **Language Independent**: Support for multiple programming languages, allowing developers to choose the best language for their use case.
- **Third party auth and services**: Plenty of third party services and authentication providers to extend functionality.
- **Faster Time to Market**: Rapid development and deployment cycles enable quicker release of features and updates.
- **Innovation and Experimentation**: Low cost and ease of use encourage experimentation and innovation.
- **Green Computing**: Efficient resource utilization leads to reduced energy consumption and environmental impact.

### Serverless Computing Constraints

- **Unsuitable for long-running processes**: Serverless functions are designed for short-lived tasks and may not be suitable for applications requiring long execution times. Benefits diminish for workloads that run continuously for extended periods.
- **Vendor lock-in risks**: Dependencies on cloud provider tools and technologies can make it difficult to switch providers or migrate applications.
- **Cold Start**: Initial invocation of a function may experience latency due to the time taken to provision resources. This can impact performance for latency-sensitive applications.
- **Latency unsuitable for time-critical apps**: Network latency and cold start times may not meet the requirements of applications that demand real-time responsiveness.
- **Security Concerns**: Attach surface moves from endpoint to source code and cloud providers' security measures may not align with organizational policies.
- **Complex Monitoring and Debugging**: Distributed nature of serverless applications can make it challenging to monitor and debug issues. It can't be imitated BaaS environment in local machine.
- **Language Support Independency**: You are limited to the languages and runtimes supported by the cloud provider.
- **Server Optimization Loss**: There are no servers to optimize for performance, as the cloud provider manages the infrastructure.
- **No state persistence**: Functions are stateless, requiring external storage solutions for maintaining state between invocations. Since local cache lasts only few hours, it is better to include external caches like redis or memcached.

### Serverless vs Containers

Serverless and Containers are not mutually exclusive. They actually work best together in a hybrid solution.
Industry Tested Advice - Build serverless first and if needed move to containers.

---

## Introduction to FasS Model

---

### What is FaaS?

- **Function as a Service**
- **Cloud computing without complex architecture**

### FaaS Characteristics

- Subset of serverless computing
- Creates the application in the form of multiple functions where a function is a piece of software written in any programming language.
- Can be deployed on hybrid-cloud as well as on-premise environments.
- Stateless but can maintain state using external caches.
- Functions execute in milliseconds and process individual requests in parallel, thus making them instantaneously scalable.
- Lightweight and uses decoupling architecture mechanism.
- Build on time taken to run functions and not on server instance sizes.

### FaaS Benefits

- Divides server into functions, that can be scaled automatically and independently so you don't have to manage infrastructure.
  - Focus more on code
  - Reduces time to market
- Pay for what you use
- Functions are small,stateless and independent pieces of code
  - Scale automatically and independently as required
  - Scale down automatically if demand drops
- Inherent high availability
  - Spread across regions and availability zones
  - Can be deployed without incremental costs

### How serverless stack component work

A serverless stack comprises of three main components, namely

- FaaS (Function as a Service)
- BaaS (Backend as a Service)
- API Gateway

1. Event requests are received from different channels like HTTP request, webhooks from repository such as GitHub or DockerHub, and scheduled jobs.
2. These events go through API Gateway, which identifies and forwards them to respective functions.
3. The functions process these requests, and they are further redirected (if necessary) toward the backend services (such as file storage, object storage, block storage, notification services and so on..)
4. The output request is then sent back to the client through the FaaS component and the API Gateway.

### FaaS principles and best practices

- Make each function perform only one action
  - Make your code scope limited, efficient and lightweight
  - Make sure that functions load and execute quickly
- Avoid function chaining, since value of FaaS is in its isolation of functions.
  - Too many functions increases cost and remove the value of isolation of your function
- Limit dependencies on third-party libraries
  - Because they can slow down initialization and thus
  - Make them harder to scale

### Managed FaaS Providers

- Amazon - AWS Lambda
- Google Cloud Functions
- Microsoft - Azure Functions
- IBM Cloud Functions
- OpenShift Cloud Functions from RedHat
- Others.. such as Netlify, Oracle or trilio

### Self-managed FaaS

- _Fission_ Framework for Serverless on K8s
- _Fn Project_ A container native serverless platform
- _Knative_ A K8s platform to build, manage and deploy serverless.
- _OpenFaas_ Allows any windows or linux process into a function

---

## The Serverless Framework

---

### What is Serverless Framework?

**Serverless Framework is a free and open source web framework written using Node.js.** It was originally designed to provision AWS Lambda Functions, Events and Infrastructure Resources safely and quickly. But it is not limited to AWS. Other supported platforms are: Microsoft Azure, Google Cloud Platform and Apache OpenWhisk

Serverless framework is a CLI that offers structure, automation and best practices out-of-the-box, allowing you to build sophisticated, event-driven, serverless architecture, comprising of

- Functions
- Events
- Resources and
- Services.

### Functions

- Merely a code, deployed in the cloud, that is most often written to perform a single task.
- Each function is independent unit of execution and deployment, like a microservice.
- A Task can be
  - Saving a user to the database
  - Performing a Scheduled Job at a specified time

### Events

- Functions are triggered by Events
- For example:
  - An HTTP Request on an API Gateway URL
  - Or a new file uploaded in an S3 bucket

### Resources

- Resources are infrastructure components used by the functions
- Such as:
  - A database provided to you as a service by cloud provider
  - An S3 Bucket

### Services

- A service is a frameworks unit of organization. Think of it as project files, though you can have multiple services for single application.
- A service is configured via a `serverless.yaml` file where you can define your
  - Functions
  - Events
  - Resources to Deploy
- When deploying with framework CLI, everything in configuration file is deployed at once.

### serverless.yaml

```yaml
service: products

functions:
  productsCreate:
    events:
      - httpApi: "POST /products/create"
  productsDelete:
    events:
      - httpApi: "DELETE /products/delete"
resources:
```

### Serverless Framework - Hello World on AWS

1. Install serverless CLI

   ```sh
   npm install -g serverless
   ```

2. Create your first AWS HTTP API using python when you run serverless

   ```sh
   serverless
   ```

   Command will present you with a wizard, and when you go through it, it will provide you with a URL.

3. Change the function code to Hello World

   ```python
   def hello(event, context):
       body = "Hello World!"
       response = {"statusCode": 200, "body": body}
       return response
   ```

4. Redeploy using serverless

   ```sh
   serverless deploy
   ```

---