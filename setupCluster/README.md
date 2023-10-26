# How to setup knative on k8s cluster.
1. Install knative serving:
```
kubectl apply -f https://github.com/knative/serving/releases/download/knative-v1.11.1/serving-crds.yaml
```
```
kubectl apply -f https://github.com/knative/serving/releases/download/knative-v1.11.1/serving-core.yaml
```
2. Install networking layer:
```
kubectl apply -f https://github.com/knative/net-kourier/releases/download/knative-v1.11.2/kourier.yaml
```
```
kubectl patch configmap/config-network \
  --namespace knative-serving \
  --type merge \
  --patch '{"data":{"ingress-class":"kourier.ingress.networking.knative.dev"}}'
```
```
kubectl --namespace kourier-system get service kourier
```
3. Install knative eventing
```
kubectl apply -f https://github.com/knative/eventing/releases/download/knative-v1.11.4/eventing-crds.yaml
```
```
kubectl apply -f https://github.com/knative/eventing/releases/download/knative-v1.11.4/eventing-core.yaml
```


[ root@curl:/ ]$ curl -v "broker-ingress.knative-eventing.svc.cluster.local/knative-samples/default" \
> -X POST \
> -H "Ce-Id: 536808d3-88be-4077-9d7a-a3f162705f79" \
> -H "Ce-specversion: 0.3" \
> -H "Ce-Type: dev.knative.samples.helloworld" \
> -H "Ce-Source: dev.knative.samples/helloworldsource" \
> -H "Content-Type: application/json" \
> -d '{"msg":"Hello World from the curl pod."}'
* Couldn't resolve host 'broker-ingress.knative-eventing.svc.cluster.local'
curl: (6) Couldn't resolve host 'broker-ingress.knative-eventing.svc.cluster.local'
