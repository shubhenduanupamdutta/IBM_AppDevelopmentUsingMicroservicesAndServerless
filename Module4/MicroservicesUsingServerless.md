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
## Environment 