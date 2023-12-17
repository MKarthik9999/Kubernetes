# Kubernetes
1. kubectl get nodes -->  Lists all nodes in the cluster.
2. kubectl cluster-info --> Displays the endpoint of the Kubernetes master and services.
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

# What is a Deployment?
* Deployment is an _**abstraction**_ that allows you to _**describe the desired state of your application**_.
* When you create a deployment, you specify the desired state of your application by defining the number of replicas and other configuration parameters. Kubernetes then _**ensures that the actual state matches the desired state**_.
* If there is **any difference in them** then Kubernetes takes care of it by _**either adding or removing the pods as necessary**_.

# Important Commands related to Depoyment Pods:
> 1. _**kubectl apply -f web-app.yaml**_ --> Create/Apply/Update Deployment
> 2. _**kubectl get deployments**_ --> Check Deployment and Pods (kubectl get pods)
> 3. _**kubectl scale deployment web-app**_ --replicas=5 --> Scale Deployment
> 4. _**kubectl rollout status deployment web-app**_ --> Rollout (updating to newer versions) status
> 5. _**kubectl rollout undo deployment web-app**_ --> Rollback to previous version
> 6. _**kubectl rollout status deployment web-app**_ --> Rollback status
> 7. _**kubectl delete deployment web-app**_ --> Delete Deploymen


# What is a Replicaset?
* ReplicaSet _**ensures that a specified number of replica pods are running at any point in time**_.
* It is ***responsible for maintaining the desired replica count and managing the lifecycle of the pods***.
* They help in achieving _**high availability and scalability**_ by automatically scaling the number of replicas up or down based on the specification.
* When you create a replica set, ***you specify the desired number of replicas and provide a template for creating the pods***.

**_If we deploy pod as a normal pod then it will running as a single pod there will be no HIGH AVAILABILITY, but if we create a pod with multiple copies using a DEPLOYMENT, it provides HIGH AVAILABILITY, the deployment internally creates a REPLICA SET and the replica set ensures that the actual state matches the desired state._**

# Any manifest file (either pod or deployment or replicaset) **_there are four primary attributes:_**
1. apiVersion:
2. kind: which has the information about the kind of the maifest file (either pod or deployment or replicaset)
3. metadata:
4. spec:

