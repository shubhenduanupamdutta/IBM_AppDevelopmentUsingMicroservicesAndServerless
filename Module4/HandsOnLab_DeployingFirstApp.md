# Hands on Labs: Deploying your First Application on IBM Cloud Code Engine

---

You will now use the CLI to deploy the Hello World application.

## Step 1: Run the following command to see the list of applications that exist

```sh
ibmcloud code-engine application list
```

There will be no applications if this is the first time you are running the lab.

## Step 2: You can alternatively use the short for ibmcloud ce app in the place of ibmcloud code-engine application

```sh
ibmcloud ce app list
```

## Step 3: Deploying the Hello World Application

You will deploy the simple flask web application which serves one REST API endpoint at the root level and returns the string Hello World. The code is provided in [Project GitHub](https://github.com/ibm-developer-skills-network/danum-pythonflaskserver). Run the following command to deploy the application.

```sh
ibmcloud ce application create --name helloworld --build-source https://github.com/ibm-developer-skills-network/danum-pythonflaskserver --image us.icr.io/${SN_ICR_NAMESPACE}/helloworld --registry-secret icr-secret --port 5000
```

## Step 4: Checks

You will see that the command creates the application and also internally sets up the required infrastructure. It takes a few seconds and it finally gives a confirmation along with the URL.

Press `ctrl(Windows)/cmd(Mac)` and the link that is created. Alternatively copy the link and paste it in a browser page and press enter. The hello world application page renders as given below.

## Step 5: To get the details of the application, run the following command

```sh
ibmcloud ce app get --name helloworld
```

It gives detailed information about the application including the time of creation, resources used, number of instances etc.
