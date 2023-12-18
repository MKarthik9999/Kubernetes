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

# Kubernetes Sevices:
# What is a Kubernetes Service and why do we use it
* Normally, interms of networking if any device wants to communicate with any other devices with in the same network or outside that network it has to be happend through the IP address only.
* similarly in Kubernetes if any pod needs to communicate with other pods or to communicate outside of the kubernetes cluster it has to be happend through the IP addresses only.
* whenever we create a pod or create multiple pods within a deployment, kubernetes assigns an individual Ip address to those pods, since we know that the lifecycle of these pods is ephimeral (meaning pods dont last for long time) their IP addresses will change everytime whenever the pod is deleted and recreated, the connections that are communicating with those kinds of pods will be terminated because of the change in the IP address.
* Even though a new pod is created for communication there will be no communication because the Ip address will be different, the Ip address of the newly created pod has to be updated to whom ever it was having comminication before, to have the communication.
* It is very difficult and complex process to update new Ip address each and every time whenver a pod is deleted and recreated.
* To overcome this problem we use **_Kubernetes services_**
* so whenever we are creating a deployment _**we use selectors**_ to deploy pods in a group with a same group name, so whenever a pod is deleted and recreated it might have different Ip address but the newly created pod will still belongs to same deployment group.
* Using that Group name we can be able to commicate within the kubernetes cluster and outside the cluster.
* _**we use that group name while we create a kubernetes service**_ so that the service can be able to detect whenver a pod is deleted and recreated it can be able to detect those pods with the help of the group name(selectors) rather than using the IP addresses.
* so, whenever a new request is arrived to kubenrnetes service it forwards that request to the pods (individual) or pods (releated to Deployment) based on the selectors mentioned while created, even though if any pods are deleted and created they will be updated because the recreated pods uses the same selector.


* ![image](https://github.com/MKarthik9999/Kubernetes/assets/88875317/afc0a91e-1e95-437c-9691-7b1c00301878)

# Types of Services in Kubernetes services:
# 1. ClusterIp:
   * It is used for internal communication within the cluster.
   * This is the default service type used by the Kubernetes service.
   * This is the most secure service type in the kubernetes services.
   * If we create a clusterIp service and if we attach that service to any of our deployments, then the pods deployed in that deployment can be able communicate with each other.
   * we can check using the following commands.
      * Find pod names using the following command:
          * _**kubectl get pods**_
      * Enter into one of the pods from the list of the pods using the following command:
          * _**kubectl exec -it <source-pod-name> -- /bin/sh**_
      * Inside that pod we can test the communication ****using the service name****:
          * _**curl internal-service:80**_
      * If we can be able to see our website deployed in the pods, then we can say that there is a communiccation between the pods.
      * we can also see it using the ip-address of the other pods and try to ping one pod from another pod
          * _**curl ip-address-of-the-destination-pod**_
# 2. Node Port:



