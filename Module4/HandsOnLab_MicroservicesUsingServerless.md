# Hands On Lab: Deploy, Update, and Scale Microservices using Serverless

---

## Static Resources

This lab uses the following static resources:

- [world_universities_and_domains.json](https://raw.githubusercontent.com/Hipo/university-domains-list/master/world_universities_and_domains.json)

---

## Task 1: Deploying the Microservice

---

### Step 1: Go to the Code engine CLI terminal

### Step 2: Clone The Repository

In the Code Engine CLI, clone the [repository](https://github.com/ibm-developer-skills-network/gentu-microservices_practiceProj.git) by running the following command.

```sh
git clone https://github.com/ibm-developer-skills-network/gentu-microservices_practiceProj.git
```

### Step 3: Change to the universities directory in the project that you just cloned

```sh
cd gentu-microservices_practiceProj/universities
```

### Step 4: List to see the directories inside it each of which have the microservices that we will deploy on Code Engine

```sh
ls
```

You will see two directories listed.

- listing
- websites

The `listing` directory contains the microservice that will list all universities or a list of universities based on keyword search.

The `websites` directory contains the microservice that will provide the list of websites given a college name. You will later update the application to return websites for all colleges that match a keyword search.

### Step 5: Run the following command to deploy the `listing` as a microservice

```sh
ibmcloud ce app create --name listing --image us.icr.io/${SN_ICR_NAMESPACE}/listing --registry-secret icr-secret --port 5000 --build-context-dir listing --build-source .
```

This takes a while.

### Step 6: Get the details of the app

Now run the following command to get the details about the app. This will also list URL that you can access the endpoints through. Copy the URL.

```sh
ibmcloud ce app get -n listing
```

### Step 7: Access the endpoint

Now try to access the endpoint you copied previously by replacing it in the following command. This command will fetch all the colleges which have the name Trinity in it.

```sh
curl <your deplymenturl>/colleges/Trinity
```

This will take a while as no instances are running.

### Step 8. Now get the details of the deployment again

```sh
ibmcloud ce app get --name listing -q
```

You can see that the instances are listed now as you just accessed the endpoint. But this instance will be terminated again when there are no more requests. You can verify the same by running the same command after a gap of 5 mins.

### Step 9: the following command to deploy the `websites` as a microservice

```sh
ibmcloud ce app create --name websites --image us.icr.io/${SN_ICR_NAMESPACE}/websites --registry-secret icr-secret --port 5000 --build-context-dir websites --build-source .
```

This takes a while and once it successfully deploys, you will get a URL that you can access the endpoints through. Copy the URL.

### Step 10: Access the Endpoint

Now try to access the endpoint you copied previously by replacing it in the following command. This command will fetch all the websites for the college Trinity College of Music.

```sh
curl <your deplymenturl>/websites/Trinity%20College%20of%20Music
```

Note: %20 is URL encoding for blank space.

### Step 11: Only Exact Match Gives Result

There is no keyword search for the websites. Only if the college name exactly matches the value that is passed, the websites are fetched. Try to access the endpoint you copied previously by replacing it in the following command. This command will fetch no websites.

```sh
curl <your deplymenturl>/websites/Trinity
```

It will return nothing.

### NOTE: If resource limits error comes, you can delete the apps using the following commands and redeploy them

```sh
ibmcloud ce app delete --name <name>
```

---

## Task 2: Scale and update the microservices in the application

---

Unlike a monolithic application, having the application composed of multiple microservices is very advantageous. It allows us to scale the microservices and/or update them independently without affecting the whole application, having to redeploy it or restart it. For example, if one service is seeing a lot of hits then we can scale just that one.

In this example, we will imagine two scenarios:

- The `listings` API endpoint gets a lot of hits and has to be scaled.

- After creating the `websites` API endpoint, based on user experience, you decide to offer a keyword search instead of an exact word search.

### Step 1: Run the following command to scale the `listing` application to three instances

```sh
ibmcloud ce app update --name listing --min 2
```

This will scale the minimum number of instances to 2. At any point in time, there will be 2 instances of the application running.

### Step 2: Run the following command to see if the listing application has scaled

```sh
ibmcloud ce app get --name listing -q
```

### Step 3: Wait for the application to scale and all instances to run

Now when you run the curl command to access the endpoint, it will be much faster as the instance is already running 2 instances.

---

## Task 3: Updating the microservice

---

You will now update the microservice serving websites API Endpoint to take keyword search as a parameter instead of giving the whole college name.

### Step 1: Open app.py in IDE

### Step 2: Change Implementation of API Endpoint

Replace the implementation of the API endpoint, with the following code. This will enable the microservice to provide keyword searches for websites.
The updated code should be as below.

```python
from flask import Flask
from flask_cors import CORS
import json

app = Flask("University Websites")
CORS(app)

with open("UK_Universities.json", "r") as unifile:
    data = json.load(unifile)

@app.route("/websites/<name>")
def getCollegesWebsites(name):
    webpages = []
    for college in data:
        if name.lower() in college["name"].lower():
            for website in college["web_pages"]:
                webpages.append(website)
    return json.dumps({"Webpages": webpages},indent=4)

if __name__ == "__main__":
    app.run(debug=True, port=5000)
```

### Step 3: Run the following command to update the application

```sh
ibmcloud ce app update --name websites --image us.icr.io/${SN_ICR_NAMESPACE}/websites --registry-secret icr-secret --port 5000 --build-context-dir websites --build-source .
```

### Step 4: Access the endpoint for verification

This will update the existing application. To verify the same run the following command. You may recollect from the previous exercise that this did not return any websites as the previous code did not support keyword search.

```sh
curl <your deplymenturl>/websites/Trinity
```

You will see the websites of all colleges which have Trinity in their name listed.
