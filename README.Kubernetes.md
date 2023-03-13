Kubernetes

Kubernetes Architecture



What is ETCD:
ETCD is a distributed reliable key-value store that is simple, Secure and fast.


ETCDCTL is the CLI tool used to interact with ETCD.

ETCDCTL can interact with ETCD Server using 2 API versions - Version 2 and Version 3.  By default its set to use Version 2. Each version has different sets of commands.


Kube API Server:

The Kube API server first authenticate the request and validate it and then it retrieves the data from ETCD cluster

The scheduler continuously monitor the API server and realizes that there is a new pod with no node assigned and the scheduler assigns the right node to place the new pod to put on and communicates back to the Kube-API server and updates the information in the ETCD Cluster 

The API Server then passes that information to the kubelet in the appropriate worker node, the kubelet then creates the pod on the node and instructs the container run time engine to deploy the application image once done, the kubelet updates the status back to the api server and the api server updates the data back in the ETCD Cluster.

The Kube API server is responsible for 
	a) authenticating User
	b) Validate Request
	c) Retrieve data
	d) Update ETCD
	e) Scheduler
	f) Kubelet

The Kube API Server is the only component that interacts with the ETCD, 

Kube Controller Manager:


It manages the various controllers inside the kubernetes.

The controller continiously monitors the state of various components within the system and works towards bringing the whole system to the desired functioning state.

Ex: 
For example, the note controller is responsible for monitoring the status of the nodes and taking necessary actions to keep the applications running. It does that through the Kube API server. The node controller tests the status of the notes every five seconds. That way the node controller can monitor the health of the notes.


If it stops receiving heartbeat from a note the note is marked as unreachable but it waits for 40 seconds before marking it unreachable. After a note is marked unreachable it gives it five minutes to come back up. If it doesn't, it removes the PODs assigned to that note and provisions them on the healthy ones if the PODs are part of a replica set. The next controller is the replication controller. It is responsible for monitoring the status of replica sets and ensuring that the desired number of PODs are available at all times within the set.
If a POD dies, it creates another one.
