# MicroServiceApplicationDeployment-to-Kubernetes


1. Clone the Repository:
Clone the Online Boutique repository:
```
git clone https://github.com/GoogleCloudPlatform/microservices-demo
cd microservices-demo/
```
2. Set the Google Cloud Project and Region:
Set your project ID and region, and enable the Google Kubernetes Engine API:

```
export PROJECT_ID=<PROJECT_ID>
export REGION=us-central1
gcloud services enable container.googleapis.com --project=${PROJECT_ID}
```
Make sure to replace <PROJECT_ID> with your Google Cloud project ID.

3. Create a GKE Cluster:
Create a new GKE cluster:
```
gcloud container clusters create-auto online-boutique --project=${PROJECT_ID} --region=${REGION}
```
This will create a Kubernetes cluster in Google Cloud. It might take a few minutes for the cluster to be created.
4. Deploy Online Boutique:
Once the cluster is ready, deploy the Online Boutique application:

```
kubectl apply -f ./release/kubernetes-manifests.yaml
```
5. Check Pod Status:
After deploying, you can check the status of the pods:
```
kubectl get pods
```
You should see all the pods running, similar to this:
```
adservice-5d5bbf6857-vnw5d               1/1     Running   0                
cartservice-55b7f75449-hmhz6             1/1     Running   0                
checkoutservice-86d7fdbd84-g9c87         1/1     Running   0              
currencyservice-547f8cdb94-b2rlr         1/1     Running   12 
emailservice-85cddc866d-9bwp5            1/1     Running   2 
frontend-f76df9b89-hdhm8                 1/1     Running   0              
loadgenerator-fdd75c57b-6p9bg            1/1     Running   0                
paymentservice-77984ccb4d-28fnr          1/1     Running   12 
productcatalogservice-745f7776fb-jvlvk   1/1     Running   0                
recommendationservice-8499974949-ghm28   1/1     Running   1 
redis-cart-68f9695b48-4bp7f              1/1     Running   0                
shippingservice-58d578789b-jx646         1/1     Running   0
```
6. Access the Web Frontend:
Once the pods are running, you can access the web frontend using the external IP of the frontend service:
```
kubectl get service frontend-external | awk '{print $4}'
```
This will display the external IP. Open the web browser and navigate to http://EXTERNAL_IP.

or else , Instead of using kubectl commands to retrieve the external IP of the frontend, you can also use the Google Cloud Console to access it. Here's how:

1.Accessing the Frontend via Google Cloud Console:
2.Navigate to the Kubernetes Engine section in the Google Cloud Console.
3.Select your cluster from the list of clusters.
4.In the cluster dashboard, go to the "Services & Ingress" tab.
5.In the Services section, look for the frontend-external service. You'll notice it has a LoadBalancer type.
6.Click on the endpoint (external IP or URL) of the frontend-external service. This will redirect you to a page where you can access the web frontend of the Online Boutique app.

7. Delete the GKE Cluster:
After you're done with the demo, delete the GKE cluster:
```
gcloud container clusters delete online-boutique --project=${PROJECT_ID} --region=${REGION}
```
