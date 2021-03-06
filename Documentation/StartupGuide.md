## Hosts

Write this at the end of your hosts file:  
127.0.0.1 acme.com

On Windows it is located at
Windows\System32\drivers\etc

---

## RabbitMQ

**kubectl apply -f .\K8S\rabbitmq.yaml**

---

## Management
#### Make sure RabbitMQ is running

- Set Management Database credentials:  
**kubectl create secret generic management-db-credentials --from-literal=username='' --from-literal=password=''**


- Set Management config map:  
**kubectl apply -f .\K8S\Management\management-cm.yaml**  


- Apply Management Database deployment  
**kubectl apply -f .\K8S\Management\management-db.yaml**  


- Apply Management deployment  
**kubectl apply -f .\K8S\Management\management.yaml**  

---

## Catalog
#### Make sure RabbitMQ is running

- Set Catalog Database credentials:  
  **kubectl create secret generic catalog-db-credentials --from-literal=username='' --from-literal=password=''**


- Set Catalog config map:  
  **kubectl apply -f .\K8S\Catalog\catalog-cm.yaml**


- Apply Catalog Database deployment  
  **kubectl apply -f .\K8S\Catalog\catalog-db.yaml**


- Apply Catalog deployment  
  **kubectl apply -f .\K8S\Catalog\catalog.yaml**

---

## Booking

- Set config map:  
  **kubectl apply -f .\K8S\Booking\booking-cm.yaml**


- Apply Booking deployment  
  **kubectl apply -f .\K8S\Booking\booking.yaml**

---

## Ingress
- Apply ingress ApiGateway  
**kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.2.0/deploy/static/provider/cloud/deploy.yaml**  
Wait for ~1 minute  
**kubectl apply -f .\K8S\ingress.yaml**

---
## Dashboard  

- **kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.2.0/deploy/static/provider/baremetal/deploy.yaml**    
- **kubectl apply -f .\K8S\dashboard-adminuser.yaml**  
- **kubectl -n kubernetes-dashboard get secret $(kubectl -n kubernetes-dashboard get sa/admin-user -o jsonpath="{.secrets[0].name}") -o go-template="{{.data.token | base64decode}}"**  
- **kubectl proxy**  
- Go to http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/workloads?namespace=default
