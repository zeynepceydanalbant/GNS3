
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
## Örnek Client Dosyası

```nano client.py```
terminal üzerinden bu komutu yazarak client adında bir pyhton dosyası oluşturmuş oluyoruz. Dosyanın içine kodlarımızı yazıp kaydedebiliriz.

```
import timeit
import sys
import socket

def client_program():
    host = "10.1.1.1" # baglanacagimiz server'in ip adresi
    port = 5000       #baglanacagimiz port numarasi

    client_socket = socket.socket()     #client oluşturma
    client_socket.connect((host, port)) #sunucuya baglanma

    message = input("Mesajinizi giriniz: ")


    devam = 1
    while devam != '2':                #kullanici 2 girene kadar islemlerini devam ettirme

        start = timeit.timeit()
        rtt = (end - start) * 100000   # sayaci baslatma
        client_socket.send(message.encode())      # mesaj gonderme
        data = client_socket.recv(1024).decode()  # cevap alma
        
        end = timeit.timeit()               # sayaci durdurma
        rtt = (end - start) * 100000        # geçen süre hesabı
        
        print('Round Trip Time: : ' + str(rtt))  # (rtt) sureyi yazdirma

        print("Serverdan gelen cevap : " + data) # serverdan gelen cevabi terminalde gosterme

        devam = input("Devam etmek icin 1, Cikmak icin 2 yaziniz: ") # cikis veya devam sorgusu
        if(devam == '2'):
            break

        message = input("Mesajinizi giriniz: ")
  client_socket.close()   # baglantiyi kapatma

client_program()

```

# SONUÇ

- Öncelikle ``` python3 server.py ```  komutu ile server'i çalıştırınız.
- Daha sonra diğer cihazdan  ``` python3 client.py ```  komutu ile client'i çalıştırınız.
![image](https://user-images.githubusercontent.com/45692102/128880805-03b1806a-c04d-4bd1-b5e3-3c0fc1e064e4.png)


**Benim server.py ve client.py dosyalarımda farklı kodlar olduğundan dosya ismim server3 ve client3'tür.**


