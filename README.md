# Kubernetes
# What is a Pod?
* A Pod is the smallest in Kubernetes, in Kubernetes we can’t directly deploy a container instead we create a pod and deploy a container in that pod.
* A pod can have one or more containers, one container per pod is the ideal use case, the main container might be running our main application, and other containers are used to support our main application container. _**The other containers are called sidecar containers or helper containers**_.
* In docker we create containers, and those containers are managed individually but when we create a pod in Kubernetes the containers created in those pods can be managed all at once and these containers are deployed in a shared environment so they can communicate with each other.
* Pods are typically created and managed using a higher-level abstraction such as _**Deployments, Replicasets, or statefulsets which provide additional features like scaling, Roling updates, and self-healing capabilities**_.
# Important command related to Normal Pods
> 1. kubectl get pods -> will list all the pods
> 1. kubectl get pods -o wide -> will list all the pods but with more information.
> 1. kubectl describe pods -> will describe more information about pods.
> 1. Kubectl apply -f <file-name.yml> -> To create a pod from a file
> 1. kubectl delete pods < pod-name > -> deletes a pod
> 1. kubectl delete pods --all -> deletes all pods in the namespace
> 1. kubectl port-forward < pod-name > < local-port >:< container-port > -> helps to expose our application to outside world

# What is a Replicaset?
* ReplicaSet _**ensures that a specified number of replica pods are running at any point in time**_.
* It is ***responsible for maintaining the desired replica count and managing the lifecycle of the pods***.
* They help in achieving _**high availability and scalability**_ by automatically scaling the number of replicas up or down based on the specification.
* When you create a replica set, ***you specify the desired number of replicas and provide a template for creating the pods***.

# Important Commands related to Replicaset Pods:


