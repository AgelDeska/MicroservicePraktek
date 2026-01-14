# Setup Kubernetes

Panduan ini menjelaskan cara setup Kubernetes untuk proyek Perpustakaan Microservice.

## Prasyarat
- Kubernetes cluster (Minikube, Kind, atau cloud provider)
- kubectl terinstal

## Langkah Setup

1. **Buat Namespace**:
   ```bash
   kubectl create namespace perpustakaan-ns
   ```

2. **Deploy Infrastruktur**:
   - MongoDB:
     ```bash
     kubectl apply -f kubernetes/mongodb-deployment.yaml
     kubectl apply -f kubernetes/mongodb-pvc.yaml
     kubectl apply -f kubernetes/mongodb-secret.yaml
     ```
   - RabbitMQ:
     ```bash
     kubectl apply -f kubernetes/rabbitmq-deployment.yaml
     ```

3. **Deploy Services**:
   Untuk setiap service, jalankan:
   ```bash
   kubectl apply -f eureka-deployment.yaml
   kubectl apply -f api-gateway-deployment.yaml
   kubectl apply -f buku-service-deployment.yaml
   kubectl apply -f anggota-service-deployment.yaml
   kubectl apply -f notification-service-deployment.yaml
   kubectl apply -f peminjaman-query-service-deployment.yaml
   kubectl apply -f peminjaman-service-deployment.yaml
   kubectl apply -f pengembalian-service-deployment.yaml
   ```

4. **Verifikasi Deployment**:
   ```bash
   kubectl get pods -n perpustakaan-ns
   ```

## Troubleshooting
- Jika pod tidak start, cek logs: `kubectl logs <pod-name> -n perpustakaan-ns`
- Pastikan image Docker tersedia di registry lokal.