# Create and Deploy Microservices using Serverless (IBM Cloud Code Engine)

---

## IBM Cloud Code Engine

---

### Challenges of self-hosting microservices

- Deliberated Configuration and Build
- Manage Infrastructure (Servers, Containers, etc.)
- Dynamic Scaling (Up and Down)
- Communication and Security
- Monitoring and Logging (Dashboards, Alerts, etc.)

There can be other challenges as well depending on the exact scenario.

### Example - Deploying a Python based Microservice

Two types of servers can be used to deploy a Python based microservice.

- WSGI (Web Server Gateway Interface) - Gunicorn, uWSGI, etc.
- ASGI (Asynchronous Server Gateway Interface) - Uvicorn, Daphne, etc.

We need to have a web server to run the Python code. The web server will listen for incoming requests and route them to the Python code. The web server will also handle the responses from the Python code and send them back to the client.

## Using IBM Cloud Code Engine

- Just push the code to cloud and it will take care of the rest.
- Fully managed serverless platform. It combines all features that are required by Platform as a Service (PaaS) and Container as a Service (CaaS) and serverless deployment models.
- Runs you workloads like microservices, containerized apps, event-driven functions, or batch jobs.

### Main Use Cases of IBM Cloud Code Engine

- **Case 1**: Application -> _Deploy_ -> Code Engine
- **Case 2**: Source -> _Build_ -> Application -> _Deploy_ -> Code Engine
- **Case 3**: Run jobs (batch jobs, etc.)

### Main Benefits of IBM Cloud Code Engine

- Focus on code and not on infrastructure.
- Go live in seconds
- Auto-scaling (including scale to zero)
- Control Access
- Secure private network
- Integrates with other IBM Cloud services

---

## Environment Configurations for Code Engine

---

Configuring the environment for your Code Engine projects is crucial for customization and security. Environmental variables play a key role, allowing you to tailor your project's environment and safeguard sensitive information like passwords and tokens.

### Best practices for handling secrets in code engine

Avoid placing passwords, tokens, or confidential details in your code, as anyone with read access to your project can easily see this information. A more secure approach is to store such secrets in your project's environment variables, where only project collaborators and administrators can access them. The access level may vary depending on the scope defined earlier for the variable.

Environment variables (env variables) can be configured as key-value pairs, usable by your application, job, or function. These variables can be defined as literal values or as references to existing secrets or configmaps. Code Engine utilizes environment variables to facilitate the use of secrets or configmaps by your job, application, or function.

### Automatically injected variables for jobs

- When running a job, Code Engine automatically injects essential environment variables into the job run instance.
- Each job run instance gets a unique index from the specified array of indices, starting from 0, assigned by Code Engine. The JOB_INDEX environment variable contains this index.
- While jobs themselves don't have URLs, CE_DOMAIN and CE_SUBDOMAIN values become handy for referencing applications that are running in the same project.
- The full external URL of this application is appName.CE_SUBDOMAIN.CE_DOMAIN. To reference the private URL of an application, use appName.CE_SUBDOMAIN.

The list of automatically injected environment variables can be found on the [IBM Cloud documentation](https://cloud.ibm.com/docs/codeengine?topic=codeengine-inside-env-vars).

### Working with environmental variables

Managing environment variables in Code Engine is a breeze, and you can do it in two ways:

1. Console method:

   - Define environment variables while creating your app, job, or function through the Code Engine console.

   - Decide if you want to create a literal environment variable or one that references an existing secret or configmap. If you want your environment variable to fully reference an existing secret or configmap or reference individual keys in an existing secret or configmap, the secret or configmap must exist.

   - Use the console for creating, updating, or deleting environment variables. Step-by-step instructions for creating, updating/modifying, or deleting environment variables can be found on the [IBM Cloud documentation](https://cloud.ibm.com/docs/codeengine?topic=codeengine-envvar) for your guidance.

2. CLI method:

   - Utilize the Code Engine CLI to create and manage environment variables.

   - Define variables when creating or updating your app, job, or function using the CLI.

   - Whether referencing configmaps or secrets or creating a literal variable, the CLI offers flexibility.

   - Before you start, ensure your [Code Engine CLI](https://cloud.ibm.com/docs/codeengine?topic=codeengine-install-cli) environment is set up.

   - The environment variables can be created, updated, or deleted using the CLI. For detailed instructions for creating, updating/modifying, or deleting when you no longer need it, see [IBM Cloud Documentation](https://cloud.ibm.com/docs/codeengine?topic=codeengine-envvar) and follow the step-by-step guide.

---

## Project, Application, Build and Jobs

---

### Project

- Represents a _group_ that contains and manages its resource and entities.
- These entities include applications, jobs, builds, configmaps, secrets, certificate for TLS HTTPs connections and more.
- One important function of the project is to provide a namespace for the entities it contains. This means that the names of entities only need to be unique within the project, not across all projects.
- Another important function is managing resources and providing access control.
- You can monitor the resource allocation for the whole Project in terms of CPU and memory usage.

### Application

- In code engine, your code will run the application. Like regular deployed apps your running app can also serve HTTP requests over REST APIs.
- Code engine also supports applications that use WebSockets and gRPC protocols.

### Build

- Mechanism to build container image from your source code.
- Code Engine supports building from _Dockerfile_.
- Alternatively it can use a _Cloud Native Builpack_ . _Buildpack_ contains executable to perform tasks such as inspecting source code, creating a build plan, or executing the build plan to produce and image.
- After your container image is built, you can deploy image to the Code Engine and create application accordingly.

### Job

- A job is one time execution of your code.
- Like an application, a job runs the executable code packaged in a container image.
- Depending on load, Code Engine will create one or more instances of the job to process the workload.
- Before you run a job in Code Engine, you can specify workload configurations that are used each time the job runs.
- Some typical jobs are:
  - Data processing jobs
  - Batch jobs
  - Scheduled jobs
  - ETL jobs
  - Machine learning jobs
  - Billing jobs

---

## Integrations of IBM Code Engine with Other Services

---

In the IBM Cloud Code Engine world, service bindings play a crucial role in granting access to IBM Cloud services for applications, jobs, and functions. This process involves linking a service instance to a Code Engine application or job, automatically incorporating credentials into the container's environment variables.

### IBM cloud code engine service binding

Service bindings act as a bridge, allowing applications, jobs, and functions in Code Engine to access the capabilities of IBM Cloud services seamlessly. By binding a service instance to your Code Engine application or job, credentials are added to the environment, making the integration smooth. The service credentials, presented as a JSON object on the service instance dashboard, become part of the application or job environment once bound.

### Binding process

You can streamline the binding process by following these steps.

- Provision the service: Before binding, you must create an instance of the service you want to connect.

- Use code engine console or CLI: Use the Code Engine console or Command Line Interface (CLI) to bind your app, job, or function to the IBM Cloud service instance.

- Service access secret: Code Engine uses a service access secret to store the specified IBM Cloud service instance's credentials securely. This secret is crucial for connecting the IBM Cloud service instance to your Code Engine app, job, or function. Code Engine handles the creation and management of this secret for you.

### Types of services you can bind

Any IBM Cloud service compatible with IBM Identity and Access Management (IAM) and utilizing service credentials can seamlessly integrate into your Code Engine workload.

#### Access requirements

Ensure you configure your Code Engine project with the necessary IAM Access policies. These policies authorize Code Engine service bindings to view service instances and manage service credentials. IAM policies are associated with a service ID.

#### Lifecycle of service binding

A service binding remains active as long as the Code Engine workload and the associated service instance are active. Unbinding or deleting a service binding removes the connection, rendering the app, job, or function unable to access the previously bound IBM Cloud service. Manual deletion is required if you want to delete the service instance.

### Conclusion

Mastering IBM Cloud Code Engine Service Binding opens opportunities for integrating robust IBM Cloud services seamlessly into your applications. Understanding the binding process, the types of services you can connect, and the lifecycle of service bindings empowers you to make the most of this essential feature for a smooth and efficient development experience.

---

## Building Container Images for Microservices

---

### What is Container?

- Standalone and executable package of software that includes everything needed to run an application: code, runtime, system tools, libraries, and settings.
- Run anywhere
- Small, fast and portable
- Perfect match for microservices architecture

### Docker

- Popular platform for developing, shipping, and running applications using containerization.
- Provides a straightforward way to package applications and their dependencies into containers.
- Main container technology used in IBM Cloud Code Engine.

### Build a Docker container image

- Create a Dockerfile
- Use docker build command to build the image from the Dockerfile
- Container is different from Container Image
  - Conatiner Image is a static file that includes the application and its dependencies. It is immutable.
  - Container is a running instance of a container image

### Push to Container Registry

- Use docker push command to push the image to a container registry
- IBM Cloud Container Registry is a private registry service for storing and managing container images.
- Container Images in the registry can be easily pulled by using unique image name. Image name includes registry URL, namespace, image name and tag. for example, `us.icr.io/my-namespace/my-image:latest`

---

## Deploying and Running Applications

---

### Deploying an application to Code Engine

- There are two modes you can use for deploying an application to Code Engine.

  1. Public/Private container registries
  2. Source code repository with Dockerfile or Cloud Native Buildpack

- IBM Cloud Console can be used to deploy the application. With just a few clicks you can deploy your application to Code Engine.
- IBM Cloud CLI can also be used to deploy the application. This is useful for automation and scripting.
- Engine will provide a URL for your application. You can use this URL to access your application.

### Run and Test your application

- If the application runs without a problem, it should be ready within several minutes.
- You can use the Console to test your application using the provided URL.

### Create an application using CLI

#### Create application using the following command

```sh
ibmcloud ce application create --name <app-name> --image <image-name> --registry-secret <secret-name>
```

#### After app is created and deployed you can test your application

```sh
ibmcloud ce app get --name <app-name> --output <output-format-of-your-application-e.g.-url>
```

Example:

```sh
ibmcloud ce app get --name helloworld --output url
```

---

## Hands on Lab

---

- [Deploying your First Application on IBM Cloud Code Engine](./HandsOnLab_DeployingFirstApp.md)

---
