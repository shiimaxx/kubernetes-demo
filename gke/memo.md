### 作業ログ

```
https://cloud.google.com/container-engine/docs/tutorials/persistent-disk/
gcloud sql tiers list
~~gcloud sql instances create wordpress-db --tier=D2~~
gcloud sql instances create wordpress --tier=db-g1-small
gcloud sql instances list

gcloud container clusters create wppd --num-nodes 3
gcloud container clusters list

gcloud compute disks create --size 200GB wordpress-disk
gcloud compute disks list

https://cloud.google.com/sql/docs/mysql/connect-container-engine
~~gcloud sql users create proxyUser cloudsqlproxy~% --instance=wordpress-db~~
~~gcloud sql instances describe wordpress-db | grep connectionName~~
~~kubectl create secret generic cloudsql-instance-credentials --from-file=credentials.json=gke-demo.json~~
~~kubectl create secret generic cloudsql-db-credentials --from-literal=username=proxyUser~~
gcloud sql users create proxyUser cloudsqlproxy~% --instance=wordpress
gcloud sql instances describe wordpress | grep connectionName
kubectl create secret generic cloudsql-instance-credentials --from-file=credentials.json=gke-demo.json
kubectl create secret generic cloudsql-db-credentials --from-literal=username=proxyUser

kubectl create -f wordpress.yaml
kubectl get pod wordpress

kubectl create -f wordpress-service.yaml
kubectl get service wpfrontend
kubectl describe service wpfrontend

http://qiita.com/minodisk/items/547741b73763f2bab6b8
kubectl describe pod wordpress

kubectl get pod -o yaml
gcloud compute ssh
docker logs
```
