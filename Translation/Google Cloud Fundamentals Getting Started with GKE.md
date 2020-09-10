# Lab: Google Cloud Fundamentals: Getting Started with GKE

## Objectives:

In this lab, you will learn how to perform the following tasks:

- Provision a Kubernetes cluster using Kubernetes Engine.
- Deploy and manage Docker containers using kubectl.

## Steps:

1. Start a Kubernetes Engine cluster

  place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE

    export MY_ZONE=[YOUR_ZONE_HERE]

  Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:

    gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

  After the cluster is created, check your installed version of Kubernetes using the kubectl version command:

    kubectl version

  The gcloud container clusters create command automatically authenticated kubectl for you.

2. Run and deploy a container

  From your Cloud Shell prompt, launch a single instance of the nginx container. (Nginx is a popular web server.)

    kubectl create deploy nginx --image=nginx:1.17.10

  View the pod running the nginx container:

    kubectl get pods

  Expose the nginx container to the Internet:

    kubectl expose deployment nginx --port 80 --type LoadBalancer

  View the new service:

    kubectl get services

  Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.

  Scale up the number of pods running on your service:

    kubectl scale deployment nginx --replicas 3

  Confirm that Kubernetes has updated the number of pods:

    kubectl get pods

  Confirm that your external IP address has not changed:

    kubectl get services

  Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.
