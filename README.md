# envoy-proxyprotocol
Using envoy as a proxy adding proxy protocol to upstream, this can be useful when an LB doesn't support proxy protocol and force to use externalTrafficPolicy=Local, the proxy will route all traffic to a service that is type ClusterIP 
