# QAgemink
Bootcamp IT BFLP 
# CI/CD
 CI/CD adalah singkatan dari Continuous Integration (CI) 
dan Continuous Delivery (CD). Kedua konsep ini 
merujuk pada praktik-praktik dalam pengembangan 
perangkat lunak yang bertujuan untuk meningkatkan 
kecepatan, kualitas, dan keandalan pengiriman 
perangkat lunak.
 CI/CD sering kali digunakan bersama-sama sebagai 
bagian dari praktik pengembangan perangkat lunak 
yang dikenal sebagai "CI/CD pipeline," yang mencakup 
langkah-langkah dari penggabungan kode hingga 
pengiriman ke produksi secara otomatis.

## Concept CI
Continuous Integration (CI):
- CI adalah praktik di mana para pengembang secara teratur 
menggabungkan kode mereka ke dalam repository bersama, seperti Git.
- Setiap kali ada perubahan kode, sistem CI akan otomatis membangun 
(compile) dan menjalankan rangkaian tes otomatis untuk memastikan bahwa perubahan tersebut tidak merusak fungsionalitas yang sudah ada.
- Tujuan CI adalah untuk mendeteksi dan memperbaiki konflik atau 
kesalahan lebih awal dalam siklus pengembangan, sehingga tim dapat  mengatasi masalah segera setelah mereka muncul.

## Concept CD
Continuous Delivery (CD):
- CD melibatkan otomatisasi seluruh proses pengiriman perangkat lunak, 
mulai dari pembangunan, pengujian, hingga penyebaran ke lingkungan 
produksi.
- Setelah perubahan lolos dari proses CI, CD memastikan bahwa perangkat 
lunak tersebut dapat dikirim ke lingkungan produksi kapan saja dengan 
cepat dan dengan risiko sekecil mungkin.
- CD menghilangkan manual dan proses yang rentan terhadap kesalahan, 
memastikan konsistensi antara lingkungan pengembangan, pengujian, dan 
produksi

## Langkah2 CI/CD 

Menggunakan koneksi dari AWS server dan Github action
1. membuat github repo
2. mkdir ".github\workflows"
3. touch main.yml
4. input code to main.yml

```
name: Push-to-EC2

# Trigger deployment only on push to main branch
on:
  push:
    branches:
      - main

jobs:
  deploy:
    name: Deploy to EC2 on master branch push
    runs-on: ubuntu-latest

    steps:
      - name: Checkout the files
        uses: actions/checkout@v2

      - name: Deploy to Server 1
        uses: easingthemes/ssh-deploy@main
        env:
          SSH_PRIVATE_KEY: ${{ secrets.EC2_SSH_KEY }}
          REMOTE_HOST: ${{ secrets.HOST_DNS }}
          REMOTE_USER: ${{ secrets.USERNAME }}
          TARGET: ${{ secrets.TARGET_DIR }}
```
5. ubah settingan di repository (settings -> secrets & variables -> actions)
6. add new repository secret
7. sesuaikan dengan yang ada di server
```
env:
          SSH_PRIVATE_KEY: ${{ secrets.EC2_SSH_KEY }}
          REMOTE_HOST: ${{ secrets.HOST_DNS }}
          REMOTE_USER: ${{ secrets.USERNAME }}
          TARGET: ${{ secrets.TARGET_DIR }}
```
8. koneksikan ke server melalui ssh
9. pastikan secret key (.pem) di direktori yang sama
10. lakukan eksekusi di terminal
```
git add .
git commit -m "commit to aws server"
git push origin main
```


> note : untuk mengetahui koneksi telah berhasil atau belum. bisa dengan melakukan callback pada file index.js di server dengan command cat