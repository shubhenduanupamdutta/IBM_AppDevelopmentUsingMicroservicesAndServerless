# Module 1 - Introduction to Microservices

Part of the Application Development Using Microservices and Serverless course.

---

## Twelve Factor App Methodology

---

### Twelve factor app methodology is suited for web-apps. It is

- frequently used with microservices. Microservices are not a requirement for twelve factor apps, but they are a good fit.

### Grouping the twelve factors

Twelve factor can be grouped according to following phases of the software delivery lifecycle

- Code
- Deploy
- Operate

### Code Factors

#### Factor 1: Codebase

- You should always track the codebase for an application in VCS, such as Git.
- There is one-to-one relationship between codebase and an app should be contained in a **single** codebase.
- However, there will be multiple deploys, or instances, of the app.
- While codebase is the same across all deployments, different app version can be present in each deployment. For example, dev or test environment can have changes that are yet to reach production.

#### Factor 5: Build, Release and Run

- This phase demonstrates how a codebase becomes a production deployment.
- **Build:** The build stage compiles the code, gathers dependencies, and then transforms the codebase into an executable unit called a build.
- **Release:** The release stage combines the build with the current configuration of the deployment so that code is ready to run.
- **Run:** Run stage implements the application.
- You should strictly separate these 3 stages. For example, code shouldn't be changeable at run time, as that would prevent those changes to be included in the build stage.

#### Factor 10: Dev/Prod parity

- Minimizes the difference between development and production environment, which is necessary for CD to quickly promote changes into production. This action reduces the chances that code runs appropriately in one environment but not the other.
- _Parity_ is particularly essential for backend services. If you use _MySQL_ database in production, you should use the same version of _MySQL_ in development. Parity helps catch problems earlier in development process.

#### Factor 2: Dependencies

- Assume an app is only as reliable as the least reliable dependency.
- As a result, twelve-factor apps do not rely on the implicit existence of any packages, dependencies or tools.
- You must explicitly declare all the dependencies. This way when a new developer grabs the codebase, there is no assumption of the environment.

### Deploy Factors

#### Factor 3: Config

- Configuration is everything that can differ between deployments. Different databases are likely used in staging and production, so the developer should configure database credentials and locations as per deployment.
- You should avoid storing configuration as constants, since they might differ among environments. You should separate configuration from code.
- Usually, configuration is stored in environment variables or configuration files, which are easy to change across environments without changing the code.

#### Factor 4: Backend Services

- Do not distinguish between local and third-party services.
- Both should be accessible via URL or other location info along with any credentials, so that a developer can easily swap out the backend service without changing the code. For example, if a database experiences problem, a new database can be spun up without changing the code.

#### Factor 6: Processes

- An app executes in an environment as one or more processes, processes should be stateless and share nothing.
- You should store persistent data in a backend service, such as a database or a file storage service, since memory and file-systems aren't shared across processes.
- If another process handles a subsequent transaction, the subsequent transaction won't have access to any data withing the prior processes. As a result, data needs to stored centrally.

#### Factor 7: Port Binding

- **Export Services by Port Binding** When you create a web-facing service, a web-server should not be injected into an app at runtime. Instead the web app should export HTTP by binding to a port and listening to incoming requests on that port.
- **Export HTTP and other services** You can use port binding for HTTP and other services.
- **Declare a web server library dependency** Binding a port is generally done in the code by declaring a web server library as a dependency.
- **Becoming backend service for other apps** Subsequently, since these app are accessible via URL, they can become backend services for other apps.

### Operator Factors

#### Factor 8: Concurrency

- **Scale an application** An application runs concurrent processes to handle increasing load.
- **Stateless processes can be spun up without creating dependencies on other processes.**

#### Factor 9: Disposability

- **Require minimal process start time and graceful termination.**
- **Quickly deploy code or config changes.**
- **Easily scale apps.**

#### Factor 11: Logs

- **App should not concern itself with storing logs.**
- **Treat logs as event stream** And application environment should handle logs as a stream of events written to standard output.
- **Execution environment captures, aggregates, and routes logs to their destination.** This action is especially beneficial when the destination is log analysis tool.

#### Factor 12: Admin Processes

- **Enable One-off management processes** such as database migrations
- **Run against a release, using same codebase and config.**
- **Part of application code** so that they remain synchronized with the application.

---

## Microservices

---

### Scaling a Microservice

- **Horizontal Scaling** Also described as _scaling out_
- **Precise Scaling** With microservices, individual components can be scaled independently, allowing for more efficient resource utilization. Done correctly, microservices require less infrastructure because they enable precise scaling of individual components based on demand.
- **Event Driven** Microservices can be designed to react to events, allowing for more flexible and responsive architectures. This can be achieved through the use of message queues or event streams.

---

## Service Oriented Architecture (SOA)

---

### What is SOA?

- Designed an built in a service provider and consumer approach.
- The services provided
  - work as discrete unit of functionality
  - integrate seamlessly
  - Easily reusable
- Each SOA consists of three components:
  - **Interface** Defines how a service provider will execute requests from a service consumer.
  - **Contract** Defines how service providers and consumers will interact with each other.
  - **Implementation** The actual code that fulfills the contract and provides the service.

### Benefits

- Increase reliability
- Supports parallel development and deployment, due to a fixed contract between the service provider and consumer.

### Drawbacks

- **Complex Design** Due to the need for clear contracts and interfaces, SOA can introduce complexity in design and implementation, and obstruct rapid app development.
- **Expensive Investment** SOA design is expensive investment, and therefore usually only suits enterprise teams, who can invest the required time and resources.

### Example

- Banking system
  - Account service
  - Transaction service
  - Notification service
  - Payment service
  - Governance service
  - Analytics service

---

## Microservices Patterns

---

Numerous pattern available for different challenges are available. For example

- Single-page Application (SPA)
- Backend for Frontend (BFF)
- Strangler
- Service Discovery

### Single-page Application (SPA)

- Enabled by more powerful browsers, faster networks, and client-side languages, many web-interfaces began incorporating all functionality into a single page, providing a more fluid user experience.
- User enters through one interface that never reloads or navigates away from initial experience.
- Updates dynamically using calls to backend REST-based services that updates portions of screen instead of redirecting to an entirely new page.
- Simplifies the front-end experience.
- Places greater performance responsibility on backend services.

### Backend for Frontend (BFF)

- While SPA works well for single channel user experience, it delivers poor results across user experience through multiple channels (e.g., mobile, tablet, desktop).
- BFF addresses this by inserting a layer between the user experience and the resources that the experience calls on.
- This design allows for customized user experience between channels.
- For example, app used on mobile will have different screen, size, display and performance limit than an app used on a mobile device.
- Supports one backend type per user interface using the best option for that interface, rather than supporting a generic backend that works with any interface, that may negatively impact frontend performance.

### Strangler Pattern

- **Manages Refactoring for Monolithic App in stages.**
- **Gets its name from _a vine that strangles a tree_.**
- **Split functional domains**
- **Replaces with new microservices per domain.**
- **Enables two application to exist side-by-side.** Overtime, the old monolithic application is gradually replaced by the new microservices.

#### Steps for Strangler Pattern

1. **Transform**

   - Create a parallel new site

2. **Coexist**
   - Allow both the old and new systems to operate simultaneously.
   - Gradually redirect traffic from the old system to the new one.
   - Monitor performance and user feedback to ensure a smooth transition.
3. **Eliminate**
   - Decommission the old system once the new one is fully operational and all traffic has been migrated.

### Service Discovery Pattern

- Helps services and applications discover each other.
- Provides flexibility, because in a microservice, individual services can be added, removed, or updated without impacting the entire system.
- Could be used by load balancer to perform health checks and rebalance traffic on service failures.

### Other Patterns

- **Entity and aggregate patterns**
  - Example: e-commerce site
- **Adapter Patterns**
  - Helps translate relationship between incompatible objects.
  - Example: Integration with third-party payment gateways/ APIs

---

## Microservice Anti-Patterns

---

**While there are many patterns for doing microservices well, an equally significant number of patterns exist that can quickly get any development team into trouble. The following are some of the don’ts while developing microservices:**

### Don’t build microservices

The first rule of microservices is don’t start with microservices. When you determine that the monolithic application's complexity negatively affects application development and maintenance, consider refactoring that application into smaller services.

When the application becomes too large to update and maintain easily, these microservices will become ideal for breaking down the complexity and making the application more manageable.

However, until you feel that pain, you don’t even have a monolith that needs refactoring.

### Not taking automation seriously

If you have a monolith application, you only need to deploy one piece of software. Once you move to a microservices architecture, you will have more than one application with each having different code, test, and deploy cycles.

Attempting to build microservices without either:

- proper deployment and monitoring automation, or
- managed cloud services to support your now sprawling, heterogenous infrastructure

is asking for a lot of unnecessary trouble.

So, when you are building microservices, always use DevOps or cloud services.

### Don’t build nanoservices

If you go too far with the micro in microservices, you could easily find yourself building nanoservices! The complexity of which will outweigh the overall gains of microservices architecture.

Lean toward creating larger services and create smaller services when:

- Deploying changes becomes difficult
- The common data model becomes overly complex
- Loading and scaling requirements no longer synchronize and affect application performance

### Don’t turn into SOA

The two concepts; microservices and service-oriented architecture (SOA) are often confused with one another because, at their most basic level, both build reusable individual components that can be consumed by other applications.

However, microservices are fine-grained with independent data storage for each, that is, the bounded context.

A microservices project that morphs into an SOA project will likely buckle under its own weight.

### Don’t build a gateway for each service

Instead of implementing end-user authentication, throttle, orchestrate, transform, route, and analytics in each service, you should use an API Gateway.

An API gateway is an API management tool that sits between a client and your collection of backend services.

This will become central to the above-mentioned non-functional concerns and will avoid re-engineering them with each service.

### Conclusion

The aim of microservices is to solve the three most frequent challenges, that is, enhance customer experience, be flexible to new requirements, and reduce costs by providing business functions as fine-grained services.

But while doing so, you should avoid the pitfall of the above-mentioned anti-patterns making microservices a nuisance to your development, delivery, and management requirements.
