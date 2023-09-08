# Kubernetes

- What is K8s? A system to deploy containerized applications
- Nodes are individual machines (or VM’s) that run containers
- Masters are machines (or VM’s) with a set of programs to manage nodes
- Kubernetes doesn’t build our images. It fetches them from somewhere else.
- Kubernetes (the master) decides where to run each containers - each node can run a dissimilar set of containers
- To deploy something, _we update the desired state of the master with a config file_
- The master works constantly to meet your desired state
- `kubectl apply -f <filename>`: applies an object definition to the cluster
- `kubectl get <kind>`: fetches information on pods of a certain kind
- Imperative deployment: explicitly saying exactly what you want to happen on each state change. Requires a knowledge of the current state.
- Declarative deployment: saying what you want to have happen and then allowing the master to decide how to make that happen. This style of deployment is why kubernetes exists in the first place.
- When applying a configuration file, if there is an existing object with the same name and type, the master will update that existing object. If not, it will create a new object.
- `kubectl describe <object_type> <object_name>`: returns detailed information about the provided object.
- Only certain types of information can change when updating pods. Otherwise an error will be thrown.
- `kubectl delete -f <config file>`: deletes a configuration from a cluster

### Configuration

- Config files are used to make **\*\*\***objects**\*\*\***
- Each object type has a different purpose
- apiVersion: scopes the set different kinds of objects that can be used
- selector: selects an object in a cluster
  - matchLabels: used to match against another objects label
- Pods: An object that can be used to run containers. Groups together containers of very similar purpose.
  - Runs a single set of containers
  - Good for one-ff dev purposes
  - Rarely used directly in production
- Services: An object that sets up networking in a kubernetes cluster. Services have sub types.
  - NodePort: Exposes a container to the outside world. Only good for dev purposes.
  - label selector system: a system in kubernetes for defining associations between objects. One object defines a label and another selects it.
- Deployment: Maintains a set of identical pods, ensuring they have the correct config and that the right number exists
  - Runs a set of identical pods (one or more)
  - Monitors the state of each pod, updating as necessary
  - Good for development and production
  - It’s better to use deployments instead of directly using pods
  - replicas: number of pods for deployment to make
