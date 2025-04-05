# useful-k8s-manifests
A series of k8s manifests that can be used for troubleshooting 

https://stackoverflow.com/questions/52369247/namespace-stuck-as-terminating-how-do-i-remove-it
For rare situations where you need to delete namespace finalizers:

(
NAMESPACE=your-rogue-namespace
kubectl proxy &
kubectl get namespace $NAMESPACE -o json |jq '.spec = {"finalizers":[]}' >temp.json
curl -k -H "Content-Type: application/json" -X PUT --data-binary @temp.json 127.0.0.1:8001/api/v1/namespaces/$NAMESPACE/finalize
)
