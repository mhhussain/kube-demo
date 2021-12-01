# Kubernetes Basics - Cloud SIG

## Connecting to cluster

Acquire a copy of the kubeconfig file. Copy file to directory: `~/.kube`
Download `kubectl` from the internet, the command should be available at the command line once added to the system path.

Confirm connection to cluster (`kubectl` uses `~/.kube/config` by default for accessing cluster)

`kubectl get nodes`

## Creating a pod

Open up `pod.yaml` and update `<POD_NAME>` and `<APP_NAME>`. The default container is `joeziet/server` and default port is `8081`. Feel free to use your own container if you want, just be sure to update the port respectively.

Create the pod using the following command (in the same directory as `pod.yaml`):

`kubectl apply -f pod.yaml`

Pod can be viewed:

`kubectl get po`

<details>
<summary>Bash into the pod via `kubectl`:</summary>
  
  `kubectl exec -it <POD_NAME> -- /bin/bash`

  Once bashed in, you should be able be placed at a linux terminal. You can run the following few commands:

  1. View hostname (this should match the podname)

    `hostname`
  2. Curl application at localhost (update port if you're using a different app):

    `curl localhost:8081`
  3. Curl application at hostname:

    `curl <POD_NAME>`

</details>
.


Delete the pod using:

`kubectl delete po <POD_NAME>`

## Creating a ReplicaSet

Open up `rs.yaml` and update `<RS_NAME>` and `<APP_NAME>`. Update container and port if you want to, default is the same as above. Update the number of replicas to any non-negative number.

Create the replica set using the following command:

`kubectl apply -f rs.yaml`

Pod statuses can be watched as they change:

`kubectl get po --watch`

Try deleting a pod (use pod name from previous command):

`kubectl delete <POD_NAME>`


Delete the replica set:

`kubectl delete <RS_NAME>`

## Further things to try

- [ ] Deploy a different application
- [ ] Create a deployment
- [ ] Patch a deployment
- [ ] port-forward to access application from local machine
