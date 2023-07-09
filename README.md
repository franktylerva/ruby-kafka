# kafka-ruby

Deploy cert-manager to your Kubernetes cluster.
```
helm install cert-manager oci://registry-1.docker.io/bitnamicharts/cert-manager -f cert-manager/values.yaml
```

Create the certificate issuer.
```
kubectl apply -f cert-manager/issuer.yaml
```

Create the certificates.
```
kubectl apply -f kafka/certificate.yaml
```

Deploy Kafka to your Kubernetes cluster.
```
helm install kafka oci://registry-1.docker.io/bitnamicharts/kafka -f kafka/tls.yaml
```

Deploy a container for testing the Producer and Consumer.
```
kubectl apply -f kafka/ruby-pod.yaml
```

Open up a terminal and lanuch a consumer.
```
kubectl exec --tty -i ruby -- bash
cd code
./consumer.sh
```

In a separate terminal, produce some messages.
```
kubectl exec --tty -i ruby -- bash
cd code
./producer.sh
```