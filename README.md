# datascience-notebook

deploy datascience-notebook:
```bash
kubectl create deployment datascience-notebook --image=jupyter/datascience-notebook
kubectl expose deployment datascience-notebook --port=8888 --name=datascience-notebook
```

Get token:
```bash
kubectl logs deploy/datascience-notebook | grep token
```

Delete everything:
```bash
kubectl delete \
  deploy/datascience-notebook \
  svc/datascience-notebook \
  ing/datascience-notebook
```

Ingress value:
```bash
kubectl apply -f - << EOF
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: datascience-notebook
spec:
  tls:
    - hosts:
      - datascience-notebook.k8s.shubhamtatvamasi.com
      secretName: letsencrypt
  rules:
    - host: datascience-notebook.k8s.shubhamtatvamasi.com
      http:
        paths:
        - path: /
          backend:
            serviceName: datascience-notebook
            servicePort: 8888
EOF
```


---

### Docker

Start Server
```
docker-compose up
```

Open url
```
http://localhost:8888
```

Use token to login
