# WAIOps Demo with Instana and iLender App : 2 - Initial Configuration

This article explains about Initial Configuration required to do the Watson AIOps demo setup with Instana and iLender App.

The article is based on the the following.

- RedHat OpenShift 4.6.x / 4.7.x on IBM Cloud (ROKS)
- Watson AIOps 3.1.x

## 1. Deploy iLender App

Deploy iLender application in Kubernetes Cluster using the steps below.

### 1.1 Update Humio properties

Update `humioUrl` and `humioToken` properties in the file `./yaml/20-deployable-common.yaml`

```
  humioUrl: http://1.1.1.1:8080/api/v1/ingest/humio-unstructured
  humioToken: 
```

### 1.2 Apply the yaml

Apply the yaml in the Openshift or Kubernetes (OCP/IKS) clusters

```
kubectl apply -f ./yaml
```

### 1.3 Access the app

App is installed in the `ilender-ns` namespace.

You can access the application using the `EXTERNAL-IP` from node and `NodePort` from svc.
    - ex: http://1.1.1.1:30500


 `EXTERNAL-IP` and `NodePort` can be retrieved from the below commands.

```
Jeyas-MacBook-Pro:frontuiservice jeyagandhi$ kubectl get nodes -o wide
NAME             STATUS   ROLES    AGE   VERSION       INTERNAL-IP      EXTERNAL-IP       OS-IMAGE             KERNEL-VERSION       CONTAINER-RUNTIME
10.241.253.157   Ready    <none>   26d   v1.20.7+IKS   10.241.253.157   1.1.1.1   Ubuntu 18.04.5 LTS   4.15.0-144-generic   containerd://1.4.6
10.241.253.189   Ready    <none>   26d   v1.20.7+IKS   10.241.253.189   1.2.3.5   Ubuntu 18.04.5 LTS   4.15.0-144-generic   containerd://1.4.6
```

```
Jeyas-MacBook-Pro:frontuiservice jeyagandhi$ kubectl get svc
NAME                      TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)          AGE
ilender-bigbank           LoadBalancer   172.21.165.179   1.1.1.1       9090:30598/TCP   10d
ilender-creditscore       NodePort       172.21.55.156    <none>          9090:30501/TCP   10d
ilender-customerprofile   LoadBalancer   172.21.145.229   1.1.1.1   9090:32751/TCP   10d
ilender-frontweb          NodePort       172.21.44.159    <none>          9090:30500/TCP   10d
ilender-greatbank         LoadBalancer   172.21.84.144    <pending>       9090:31622/TCP   10d
ilender-loan              LoadBalancer   172.21.161.226   1.1.1.1   9090:30301/TCP   10d
ilender-loanprocessor     LoadBalancer   172.21.82.15     1.1.1.1   9090:30880/TCP   10d
ilender-openbanking       LoadBalancer   172.21.235.41    1.1.1.1   9090:31331/TCP   10d
ilender-user              LoadBalancer   172.21.43.214    1.1.1.1       9090:32427/TCP   10d
```


## 2. Install Humio

Setup Humio on a single node (16 core, 64 GB)

Refer: https://github.com/diimallya/humio-single-node

## 3. Create Slack account	

Setup free slack account and create workspace, channels and slack app.

Refer: https://github.com/ibm-gsi-ecosystem/watson-ai-ops-310-guide/tree/main/300-aiops-initial-configuration/13-slack-account-creation-and-integration

## 4. Update Event Manager Gateway

Need to update the Event Manager Gateway Filter with to allow events from Instana.

Add the below text to the `Filter` property of the Event Manager Gateway.

```
OR (Manager = \'Instana\') 
```

Refer: https://github.com/ibm-gsi-ecosystem/watson-ai-ops-310-guide/tree/main/400-configure-event-manager-gateway#user-content-2-update-filters-in-event-manager-gateway


## 5. Create ServiceNow account

#### Create ServiceNow developer instance 
https://pages.github.ibm.com/up-and-running/watson-aiops/3.1.1%20PoC%20Cookbooks/ServiceNow/#procure-a-servicenow-developer-instance

#### Installing Watson AIOps App plugin in ServiceNow Developer Instance
https://community.ibm.com/community/user/aiops/blogs/jeya-gandhi-rajan-m1/2021/09/08/snow-waiops-2-installing-waiops-app-plugin

#### Configuring Watson AIOps roles to ServiceNow users
https://community.ibm.com/community/user/aiops/blogs/jeya-gandhi-rajan-m1/2021/09/08/snow-waiops-3-configuring-waiops-roles-in-snow


## 6. Integrate Instana and Watson AIOps

Instana and Watson AIOps to be integrated. Refer the below URL.

https://community.ibm.com/community/user/aiops/blogs/jeya-gandhi-rajan-m1/2021/09/08/ins-waiops-1-integrating-instana-with-watson-aiops



## Navigation

Prev : [Overview](https://community.ibm.com/community/user/aiops/blogs/jeya-gandhi-rajan-m1/2021/09/21/waiops-ins-ilender-1-overview)

Next: [Data and Tool Integrations](https://community.ibm.com/community/user/aiops/blogs/jeya-gandhi-rajan-m1/2021/09/21/waiops-ins-ilender-3-data-tool-integration)

Home: [Overview](https://community.ibm.com/community/user/aiops/blogs/jeya-gandhi-rajan-m1/2021/09/21/waiops-ins-ilender-1-overview)


#### Released by :
- Jeya Gandhi Rajan M
- Vijaya Bhaskar R Siddareddi
- Vijay Sukthankar (Squad Leader)

Hybrid-Cloud Squad, GSI Labs

#ibmautomation
