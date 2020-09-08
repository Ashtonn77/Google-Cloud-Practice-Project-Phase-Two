# Google Cloud Fundamentals: Getting Started with GKE

## Objectives

In this lab, you learn how to perform the following tasks:

- Provision a Kubernetes cluster using Kubernetes Engine.

- Deploy and manage Docker containers using kubectl.

## Steps

1.  log in with sdk

2.  Provision a Kubernetes cluster using Kubernetes Engine

        - start a Kubernetes Engine cluster - for convenience, place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE. At the Cloud Shell prompt, type this partial command:

            export MY_ZONE=us-central1-a

        - start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:

            gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

        - after the cluster is created, check your installed version of Kubernetes using the kubectl version command:

            kubectl version

3.  Deploy and manage Docker containers using kubectl

        - from your Cloud Shell prompt, launch a single instance of the nginx container.

            kubectl create deploy nginx --image=nginx:1.17.10

        - view the pod running the nginx container

            kubectl get pods

        - expose the nginx container to the Internet:

            kubectl expose deployment nginx --port 80 --type LoadBalancer

        - view the new service

            kubectl get services

        - open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.

        - scale up the number of pods running on your service:

            kubectl scale deployment nginx --replicas 3

        - confirm that Kubernetes has updated the number of pods:

            kubectl get pods

        - confirm that your external IP address has not changed:

            kubectl get services
