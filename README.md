**Nama  : Nisrina Annaisha Sarnadi   
NPM   : 2306275960  
Kelas : B**

Refleksi
---

## 1. Perbandingan Application Logs Sebelum dan Sesudah Exposed sebagai Service

**Sebelum exposed sebagai Service:**
- Aplikasi berjalan di dalam pod tetapi tidak dapat diakses dari luar cluster
- Logs hanya menunjukkan startup aplikasi dan health checks internal
- Tidak ada traffic masuk karena tidak ada cara untuk mengakses aplikasi

**Sesudah exposed sebagai Service:**
- Ketika `minikube service hello-node` dijalankan, aplikasi menjadi dapat diakses melalui browser
- Setiap kali aplikasi dibuka di browser, akan muncul log request HTTP baru
- Jumlah log akan bertambah setiap kali dilakukan akses terhadap aplikasi karena setiap request HTTP akan tercatat

Untuk melihat logs:
```bash
kubectl logs deployment/hello-node -f
```

## 2. Perbedaan `kubectl get` dengan dan tanpa opsi `-n`

**Tanpa opsi `-n`:**
```bash
kubectl get pods,services
```
- Menampilkan pods dan services di **namespace default**
- Pods/services yang Anda buat (seperti hello-node) berada di namespace default

**Dengan opsi `-n kube-system`:**
```bash
kubectl get pods,services -n kube-system
```
- Menampilkan pods dan services di **namespace kube-system**
- Namespace kube-system berisi komponen sistem Kubernetes (seperti coredns, etcd, kube-apiserver, dll.)

**Mengapa output tidak menampilkan pods/services yang Anda buat?**

Pods dan Services yang saya buat secara eksplisit (hello-node) tidak ditampilkan karena berada di namespace **default**, sedangkan perintah dengan `-n kube-system` hanya menampilkan resource yang ada di namespace **kube-system**.