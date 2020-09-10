# Google Cloud Fundamentals: Getting Started with GKE

## Objectives:
In this lab, you will learn how to perform the following tasks:
 - Provision a Kubernetes cluster using Kubernetes Engine.
 - Deploy and manage Docker containers using kubectl.

## Steps: 

1. Sign in to the Google Cloud Platform (GCP) Console

2. In GCP console, on the top right toolbar, click the Open Cloud Shell button.

3. Confirm that needed APIs are enabled
   
   - Get a list of all enabled services
      ```
      gcloud services list --available
      ```
   - Scroll down in the list of enabled APIs, and confirm that both of these APIs are enabled:
      - Kubernetes Engine API (container.googleapis.com)
      - Container Registry API (containerregistry.googleapis.com)
	  
   - If either API is missing, type the following command to enable both APIs
      ``` 
      gcloud services enable container.googleapis.com
	  
	  gcloud services enable containerregistry.googleapis.com
      ```
4. Start a Kubernetes Engine cluster

   - To display a list of all the zones in the region to which Qwiklabs assigned you, enter this partial command 
      ```
      gcloud compute zones list | grep us-central1
      ```
   - Place your assigned zone in an environmental variable
      ```
      export MY_ZONE=us-central1-a
      ```
   - Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:
      ```
      gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
      ```
   - After the cluster is created, check your installed version of Kubernetes using the kubectl version command:
      ```
      kubectl version
      ```
   - View your running nodes 
	  ```
      gcloud compute instances list
      ```
	  
	Your Kubernetes cluster is now ready for use.
	
5. Run and deploy a container

   - From your Cloud Shell prompt, launch a single instance of the nginx container. (Nginx is a popular web server.)
      ```
      kubectl create deploy nginx --image=nginx:1.17.10
      ```
   - View the pod running the nginx container:
      ```
      kubectl get pods
      ```
   - Expose the nginx container to the Internet:
      ```
      kubectl expose deployment nginx --port 80 --type LoadBalancer
      ```
   - View the new service:
      ```
      kubectl get services
      ```
	  
	  You can use the displayed external IP address to test and contact the nginx container remotely.

	  It may take a few seconds before the External-IP field is populated for your service. This is normal. Just re-run the kubectl get services command every few seconds until the field is populated.
	  
	  Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.

   - Scale up the number of pods running on your service:
      ```
      kubectl scale deployment nginx --replicas 3
      ```
   - Confirm that Kubernetes has updated the number of pods:
      ```
      kubectl get pods
      ```
   - Confirm that your external IP address has not changed:
      ```
      kubectl get services
      ```
	  
	  Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.
 