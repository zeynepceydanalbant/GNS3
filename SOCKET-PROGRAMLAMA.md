
# GNS3 Üzerinde Socket Programlama


![image](https://user-images.githubusercontent.com/45692102/128874116-ec535499-ade5-42af-ad93-cc06d41f2f0a.png)

Topolojimizde 1 switch ve iki  ubuntu dockerimiz var.

Socket programlamayı python üzerinden yapmak istediğim için öncelikle cihazları internete bağlayıp gerekli güncellemeleri yaptım ve dosyaları indirdim. Eğer python kurulu değilse bu adımı GNS3 readme dosyasından öğrenebilirsiniz.

Daha sonra cihazlara kolayca ulaşabilmek için statik ip verdim. Bunu şu şekilde gerçekleştirdim;

- nano /etc/network/interfaces 
- ![image](https://user-images.githubusercontent.com/45692102/128875343-2af43320-b044-4795-82a4-69c865ad514b.png)
- Görüldüğü üzere auto eth0 ve iface eth0 inet static kısımlarındaki # işaretini kaldırarak etkinleştirdim
- address kısmında cihazlarımdan server olana 10.1.1.1 client olana 10.1.1.2 ip adreslerini verdim. İstediğiniz ip'yi verebilirsiniz.

Bu şekilde kolayca nasıl ulaşabileceğimi belirlemiş oldum.

# Server.py Dosyasının Oluşturulması

```nano server.py```
terminal üzerinden bu komutu yazarak server adında bir pyhton dosyası oluşturmuş oluyoruz. Dosyanın içine kodlarımızı yazıp kaydedebiliriz.

## Örnek Server Dosyası
```
#!/usr/bin/env python3

import socket

HOST = "10.1.1.1"      #serverimizin ip adresi
PORT = 5000            #soket sunucu bağlantı portumuz

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:   # soket olusturma
 s.bind((HOST, PORT))          #  soketin ip ve port numaralarinin belirtilmesi                            
 s.listen()                    # belirtilen ip ve port numaralarinin dinlenmesi
 conn, addr = s.accept()       # soket baglantisini onaylama
 with conn:
  print('Baglanti: ', addr)    # baglantiyi ekrana yazdirma
  while True:

      data = conn.recv(1024)   # client tan gelen veriyi yakalama
      x = str(data)            # gelen veri

      print(x)


      if not data:             # data yoksa donguyu durdurma
          break
      cevap= input("Client'e mesajiniz:")                       #client'a göndermek istediğimiz mesaj
      conn.sendall(str(cevap).encode())                         # mesajı serverdan client a cevap olarak iletme
```



