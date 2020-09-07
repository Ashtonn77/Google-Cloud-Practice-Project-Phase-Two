# LAB: Google Cloud Fundamentals: Getting Started with Compute Engine

## Objectives:

In this lab, you will learn how to perform the following tasks:

    - Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

    - Create a Compute Engine virtual machine using the gcloud command-line interface.

    - Connect between the two instances.

## Steps:

1.  Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console:

        gcloud compute instances create my-vm-1 --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default" --tags http

        gcloud compute firewall-rules create allow-http --action=ALLOW --destination=INGRESS --rules=http:80 --target-tags=http

2.  Create a Compute Engine virtual machine using the gcloud command-line interface

    - choose a zone from the listed zones and use the grep command to filter
      gcloud compute zones list | grep us-central1

      gcloud config set compute/zone us-central1-b
      gcloud compute instances create my-vm-2 --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"

3.  Connect between the two instances

    3.1 Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:

    - connect yo my-vm-2:
      gcloud compute ssh my-vm-2

    - ping my-vm-1 from my-vm-2:
      ping -c 4 my-vm-1

    - use ssh command to open command prompt for my-vm-1 from my-vm-2
      ssh my-vm-1

    - at the my-vm-1 command prompt, install the Nginx web server
      sudo apt-get install nginx-light -y

    - use the nano text edior to add a message to the home page of the server:
      sudo nano /var/www/html/index.nginx-debian.html

    - use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:
      Hi from Ashton

    - exit nano editor

    - confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
      curl http://localhost/

      - result: the response will again be the HTML source of the web server's home page, including your line of custom text

    - to exit the command prompt on my-vm-1, execute this command
      exit

    - you will return to the command prompt on my-vm-2. to confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
      curl http://my-vm-1/ - result: the response will again be the HTML source of the web server's home page, including your line of custom text

      3.2 Get external ip-address of the my-vm-1 instance:

      gcloud compute instances list --zone us-central1-a

      3.3 Copy the external ip-address of the my-vm-1 instance and paste it into a new browser tab - result: the response will again be the HTML source of the web server's home page, including your line of custom text
