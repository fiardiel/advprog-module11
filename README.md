# ADVPROG Module 11

## Reflection 1

1. Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?
![ss1](img/ss1.png)
**Answer:**
    The number of logs increase each time I open the app. It increases by 2 since every time I open the app the HTTP get method appears twice in the log. This is due to the first get method is to get the favicon and the second get method is to get the index.html.


2. Notice that there are two versions of kubectl get invocation during this tutorial section. The first does not have any option, while the latter has -n option with value set to kube-system. What is the purpose of the -n option and why did the output not list the pods/services that you explicitly created?
**Answer:**
    The -n option is used to specify the namespace to list the pods/services. The output did not list the pods/services that I explicitly created because the namespace is set to kube-system. The pods/services that I created are in the default namespace.

## Reflection 2

1. What is the difference between Rolling Update and Recreate deployment strategy?
**Answer:**
    Rolling Update is a deployment strategy that updates the pods in a rolling fashion. It updates the pods one by one and waits for the new pod to be ready before terminating the old pod. This ensures that the application is always available during the update. On the other hand, Recreate deployment strategy terminates all the pods at once and creates new pods with the updated version. This strategy is faster but the application will be unavailable during the update.

2. Try deploying the Spring Petclinic REST using Recreate deployment strategy and document your attempt.
**Answer:**
    First, in the `deployment.yaml` file, I changed the strategy to type: Recreate. I then deployed the Spring Petclinic REST using Recreate deployment strategy by running the following command:
    `kubectl apply -f deployment.yaml`. The deployment was successful and the pods were created. However, the application was unavailable during the update. The application was only available after the new pods were created.

3. Prepare different manifest files for executing Recreate deployment strategy.
**Answer:**
```
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "4"
  creationTimestamp: "2024-05-15T06:35:26Z"
  generation: 5
  labels:
    app: spring-petclinic-rest
  name: spring-petclinic-rest
  namespace: default
  resourceVersion: "6635"
  uid: e6630eee-8573-46c0-a901-1ea4e21763a9
spec:
  progressDeadlineSeconds: 600
  replicas: 4
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: spring-petclinic-rest
  strategy:
    type: Recreate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: spring-petclinic-rest
    spec:
      containers:
      - image: docker.io/springcommunity/spring-petclinic-rest:3.2.1
        imagePullPolicy: IfNotPresent
        name: spring-petclinic-rest
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
status:
  availableReplicas: 4
  conditions:
  - lastTransitionTime: "2024-05-15T09:52:23Z"
    lastUpdateTime: "2024-05-15T09:52:23Z"
    message: Deployment has minimum availability.
    reason: MinimumReplicasAvailable
    status: "True"
    type: Available
  - lastTransitionTime: "2024-05-15T07:44:13Z"
    lastUpdateTime: "2024-05-15T09:52:53Z"
    message: ReplicaSet "spring-petclinic-rest-54f476f68" has successfully progressed.
    reason: NewReplicaSetAvailable
    status: "True"
    type: Progressing
  observedGeneration: 5
  readyReplicas: 4
  replicas: 4
  updatedReplicas: 4

```
    

4. What do you think are the benefits of using Kubernetes manifest files? Recall your experience in deploying the app manually and compare it to your experience when deploying the same app by applying the manifest files (i.e., invoking `kubectl apply -f` command) to the cluster.

**Answer:**
    The benefits of using Kubernetes manifest files are:

- It is easier to deploy the application to the cluster. The manifest files contain all the necessary configurations for the deployment.

- It is easier to manage the deployment. The manifest files can be version controlled and changes can be tracked.

- It is easier to scale the application. The manifest files can be updated to increase the number of replicas.

- It is easier to update the application. The manifest files can be updated to use a new version of the application.
    
- It is easier to rollback the application. The manifest files can be updated to use a previous version of the application.