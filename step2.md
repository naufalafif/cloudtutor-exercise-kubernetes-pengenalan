### Menggunakan Kubernetes

Kami sudah menyiapkan local cluster menggunakan kind

Pertama mari kita cek apakah cluster sudah berjalan. Untuk mengecek status cluster, kita bisa menggunakan tool `kubectl` dengan perintah berikut

```{.bash .copy}
kubectl cluster-info
```

```{.bash}
Kubernetes control plane is running at https://127.0.0.1:41101
CoreDNS is running at https://127.0.0.1:41101/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
```

Ini menunjukan bahwa cluster sudah berjalan dan menampilkan informasi url dari komponen kubernetes

#### Mendeploy Aplikasi

Salah satu cara mudah untuk mendeploy aplikasi adalah dengan menggunakan perintah `create`, perintah tersebut akan menjalankan aplikasi tanpa harus menyiapkan file JSON ataupun YAML

```{.bash .copy}
kubectl create deployment fastapi --image=naufalafif58/fastapi-app --port=8080
```

- `--image=naufalafif58/fastapi-app` adalah image yang digunakan
- `--port=8080` digunakan untuk memberitahukan kubernetes bahwa aplikasi berjalan di port 8080

Selanjutnya kita bisa mengecek status aplikasi menggunakan perintah `get deployment`

```{.bash .copy}
kubectl get deployment
```

```{.bash}
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
fastapi   1/1     1            1           50s
```

> Apabila aplikasi belum berjalan atau `AVAILABLE`, maka tunggu beberapa saat dan cek kembali

Perhatikan kolom `READY` dan `AVAILABLE`, kedua kolom ini memberikan informasi tentang status dari aplikasi baru saja kita deploy. `AVAILABLE` menunjukan berapa instance dari aplikasi yang tersedia dan `READY` menunjukan informasi yang sama plus total jumlah instance.

#### Mengakses Aplikasi

Ketika sebuah deployment dibuat, Kubernetes akan menjalankan aplikasi dalam node yang terpisah dari jaringan host. Bagaimana cara mengakses aplikasi ? diperlukan komponen tambahan yaitu `service`

Service adalah komponen yang digunakan untuk meng-expose `deployment` agar dapat diakses dari luar `node`. Gunakan perintah berikut untuk mengakses deployment

```{.bash .copy}
kubectl expose deployment fastapi --type=LoadBalancer --name fastapi-http
```

```{.bash}
service/fastapi-http exposed
```

Selanjutnya kita bisa mengecek status service menggunakan perintah `get service`

```{.bash .copy}
kubectl get service
```

**Penting**: local cluster tidak memiliki loadbalancer bawaan seperti halnya cloud provider.

Jalankan perintah berikut untuk mem-forward service ke host

```{.bash .copy}
kubectl port-forward service/fastapi-http 8000:8080
```

Kita bisa mengecek aplikasi pada URL dibawah

```{.bash .copy}
https://#ID#-8000.host.cloudtutor.io
```
