# Jenkins CI/CD

## Langkah 4: Implementasi CI/CD dengan Jenkins
Jenkins digunakan untuk mengotomatisasi proses Build (Maven), Containerize (Docker), dan Deployment (Kubernetes Update).

## Setup Jenkins di Kubernetes

### Deploy Jenkins
Masuk ke folder kubernetes/jenkins:
```bash
kubectl apply -f jenkins-setup.yaml
kubectl apply -f jenkins-pvc.yaml
kubectl apply -f jenkins-deployment.yaml
```

### Akses Jenkins
Buka http://localhost:32000

## Konfigurasi Pipeline
Setiap microservice memiliki file Jenkinsfile sendiri. Pipeline melakukan langkah berikut:

- **Initialize**: Setup Docker & Kubectl client.
- **Build Maven**: mvn clean package -DskipTests.
- **Build Docker**: Membuat image baru dengan tag versi.
- **Push Image**: Upload ke Local Registry (localhost:5000).
- **Deploy**: Update image di deployment Kubernetes dan melakukan rollout restart.

## Daftar Pipeline
- Pipeline-bukuservice
- Pipeline-anggotaservice
- Pipeline-peminjaman-command
- Pipeline-peminjaman-query
- Pipeline-pengembalian-service
- Pipeline-notification-service