## Ingress
Suppose, you have an website for shopping, you created a service(LB) for accessing outside cluster. So you need to point your dns name to www.shopping.com

If there was separate section for kids, you need to craete another service(LB) for kids and point to it. In this way, service LB will be increased , cost and complexity too.

We can do all of the above configuration within K8 cluster as a K8 definition file i.e., Ingress.

Ingress is a Layer-7 built which helps users access your application using a singhle URL that you configure to route traffic to different services and to implement SSL security.

Ingress mainly consists of 2 objects:
1. Ingress Resources: It is created using definition files. It configures Ingress to route traffic to other services, forward incoming traffic to a single application, route user based on domain name.
2. Ingress Controller: It deploys services like Nginx, HAProxy on your K8 Cluster.
- Write deployment yaml file to create Nginx image.
- A service to expose it.
- A configmap to feed Nginx Configuration data.
- A Service Account with right permissions to access all of these objects.
```
//If you have a single backend.
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-wear
spec:
  backend:
    service:
      name: svc-1
    port:
      number: 8080

//Route based on different URL's
spec:
  rules:
  - http:
    paths:
    - path: /wear
      backend:
        service:
          name: svc-1
        port:
          number: 8080
    - path: /tear
      backend:
        service:
          name: svc-2
        port:
          number: 80

//Route based on Domains
spec:
  rules:
  - host: shirts.buy.com
    http:
      paths:
      - backend:
           service:
              name: svc-1
            port:
              number: 80
   - host: watch.buy.com
      http:
        paths:
        - backend:
             service:
                name: svc-2
              port:
                number: 80
```

If a user tries to access URL that doesn't match any of these rules, iuser is directed to default backend.
