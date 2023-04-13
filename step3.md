### Scaling Aplikasi

Sebelumnya kita sudah menjalankan aplikasi menggunakan deployment & meng-expose nya menggunakan service. Sekarang kita akan melalukan scaling aplikasi menjadi beberapa instance

Untuk men-scale atau mengubah jumlah aplikasi yang dijalankan, kita bisa menggunakan perintah `scale` seperti berikut

```{.bash .copy}
kubectl scale deployment fastapi --replicas=3
```

```{.bash}
deployment.apps/fastapi scaled
```

Kita telah mengirim perintah pada Kubernetes untuk menjalankan 3 aplikasi fastapi. Penggunaan `--replicas` adalah untuk menentukan berapa jumlah instance yang diinginkan, apabila sudah terdapat aplikasi yang berjalan maka Kubernetes akan menyesuaikan berapa jumlah aplikasi yang perlu ditambahkan.

#### Mengecek Hasil Scaling

Untuk mengecek status scaling, gunakan kembali perintah `get deployments`

```{.bash .copy}
kubectl get deployments
```

Sekarang kolom `READY` dan `AVAILABLE` memiliki value yang berbeda dari sebelumnya yaitu `3`.

Kita bisa mengecek detail dari aplikasi yang ditambahkan menggunakan perintah `get pods`

```{.bash .copy}
kubectl get pods
```

```{.bash}
NAME                     READY   STATUS    RESTARTS   AGE
fastapi-57c4d74858-d284g   1/1     Running   0          94s
fastapi-57c4d74858-tflb8   1/1     Running   0          7m9s
fastapi-57c4d74858-wfgmb   1/1     Running   0          94s
```

Perhatikan kolom `AGE`, salah satu pod memiliki age yang berbeda dari kedua pod lainnya. Ini menunjukan bahwa kedua pod tersebut adalah pod baru yang ditambahkan pada proses scaling sebelumnya

Kita sudah mencoba menggunakan beberapa fungsi dasar pada Kubernetes, pada exercise selanjutnya kita akan belajar cara membuat file yaml dari komponen - komponen tadi (pods, deployment, service, scaling)
