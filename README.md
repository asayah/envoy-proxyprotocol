# envoy-proxyprotocol
Using envoy as a proxy adding proxy protocol to upstream, this can be useful when an LB doesn't support proxy protocol and force to use externalTrafficPolicy=Local, the proxy will route all traffic to a service that is type ClusterIP 



# Deploy the envoy proxy
```
kubectl apply -f proxy -n gloo-system
```
At this point you will have a service type LoadBalancer routing all the traffic to a service called "gateway-proxy", (Gloo Edge), and the proxy will add proxy protocol


# Install Gloo Edge 

```
helm install gloo gloo/gloo --namespace gloo-system --create-namespace --values gloo/values.yaml
```
This will configure gloo edge to use proxy protocol, and will configure the access logs so we can check the requests. 


# Test the Config

First, let's install a vs that will route to a demo service (postman echo)

```
kubectl apply -f gloo/demo -n gloo-system 
```

Make some calls to the proxy svc, you can get the IP or address by using 
```
kubectl get svc proxy -n gloo-system 
```

You should see the logs now in Gloo Edge with the correct client IP
```
kubectl logs -n gloo-system deploy/gateway-proxy
```