# Hands On Lab: Deploying your first docker image on Code Engine using Python

---

## Task 1: Deploying the docker image

---

### Step 1: Go to the Code engine CLI terminal

You will now use the CLI to deploy the Hello World application.

### Step 2: Run the following command to see the list of applications that exist

```sh
ibmcloud ce app list
```

### Step 3: Clone the code from github

```sh
git clone https://github.com/ibm-developer-skills-network/danum-pythonflaskserver
```

### Step 4: Change directory to the cloned repository

```sh
cd danum-pythonflaskserver
```

### Step 5: Build Container Image from the Dockerfile

```sh
docker build . -t us.icr.io/${SN_ICR_NAMESPACE}/helloworld2
```

### Step 6: Push the image to the namespace, so that you can run it

```sh
docker push us.icr.io/${SN_ICR_NAMESPACE}/helloworld2
```

### Step 7: Create the application

Now that the image is all set to be deployed, run the following command. Please note that since we already built and pushed the image, we can create the application without mentioning the build source. You will see that the command creates the application and also internally sets up the required infrastructure. It takes a a few seconds and it finally gives a confirmation along with the URL.

```sh
ibmcloud ce application create --name helloworld2 --image us.icr.io/${SN_ICR_NAMESPACE}/helloworld2 --registry-secret icr-secret --port 5000
```

### Step 8: Access the application

Press ctrl(Windows)/cmd(Mac) and the link that is created. Alternatively copy the link and paste it in a browser page and press enter. The hello world application page renders as given below.

---

## Task 2: Personalize the message and deploy

---

### Step 1: Personalize the message

Go to the file menu, open `danum-pythonflaskserver/app.py` and change the message from “Hello World” to “Hello yourname!”.

### Step 2: Build the docker image

```sh
docker build . -t us.icr.io/${SN_ICR_NAMESPACE}/helloworld2
```

### Step 3: Push the image to the namespace

```sh
docker push us.icr.io/${SN_ICR_NAMESPACE}/helloworld2
```

### Step 4: Update the application

```sh
ibmcloud ce application update --name helloworld2 --image us.icr.io/${SN_ICR_NAMESPACE}/helloworld2 --registry-secret icr-secret --port 5000
```

### Step 5: Access the application to see the changes
