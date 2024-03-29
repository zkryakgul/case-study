# Mini Cluster

## Table of Contents
- [Summary](#summary)
- [Details](#details)
- [Solution](#solution)

## Summary
Imagine that you have a kubernetes cluster. This cluster orchestrates many services behind the load balancer.

## Details
- Clone the GitHub repo on your local which is specified as [sample-app](sample-app/).
- Create a docker file for building a python web app within the docker image.
- You need to create a DockerHub account for uploading image.
- Build a docker image and upload this to the DockerHub.
- End to End HTTP communication is Ok for this case study.
- Create a kubernetes definition file for :
     - Create one ingress for handling HTTP requests from outside the cluster 
     - Create one service for load balancing across the pods 
     - Create a deployment with two pods that are hosting our app instances from DockerHub (which is you've uploaded).
     - Create the necessary resources for deploying postgresql 14. Make sure the data is persistent. 
- You should be able to test the application with the following URL pattern with HTTP GET request when you complete it :
     - > http://{{IP}}:{{Port}}/

- You could prepare one-click install script file as bash to install and run the mini-cluster.

## Solution
Design a system that contains all rules in the details and please make a readme file to explain your solution. You could also draw diagrams and flow charts. You could use any software language, platform, tool, library, or framework except those specified as required in the details section. Please push your solution to GitHub and share the related URL with us.

## Bonus
- Create a jenkinsfile that automates build and deploy process. Feel free to write some comment lines on it!
