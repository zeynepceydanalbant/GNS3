# GNS3


## GNS3 Nedir?
GNS3(Graphical Network Simulator) açık kaynak kodlu bir emülatör  programıdır. Cisco Router/Switch gibi ağ cihazlarını emüle ederek kompleks ağ tasarımları yapmamıza izin verir.
-  GNS3 VMWare ile stabil çalıştığını açıklamaktadır.
-  Kurulum için VMware player,vix, GNS3 VM e ihtiyaç vardır. (VMware yeni sürümlerinde vix paylaşmamıştır ekstra işlem gerektirir.)
-  Kurulum sırası başlangıçta GNS3 ve VMware player daha sonra GNS3 VM aktifleşecek ve sıra onu kurmaya gelecek. Bu işlemlerden sonra GNS3 VMware'i bulamadığını söyleyecek GNS3yi kapatıp VMware vix'i çalıştırdıktan sonra tekrar GNS3'yi açınız ve Setup Wizard kısmında ilerlediğinizde GNS3 VM bağlantısını görmüş olacaksınız.
-  Eğer hala sorun yaşıyorsanız GNS3 preferences kısmında GNS3 VM ayarları kısmına geliniz."Enable the GNS3 VM" in seçili olduğundan emin olunuz.

## Loopback Nedir, Nasıl Eklenir?
 
 Loopback terimi genel olarak modemin elektronik sinyallerinin bazı metotları ve presödürleri tanımlaması şeklinde açıklanabilir. Dijital veri akışları veya diğer maddelerin akmasını bundan kaynaklanan fasilitelerin kasıtlı işlemede ve modifikasyon dışında hızlı bir şekilde benzer kaynaklara aktarılmasıdır.
 Bir yönlendiricide loopback arayüzü yapılandırmanın bir kaç nedeni vardır. Öncelikle fiziksel bir port olmadığından yönlendirici çalıştığı sürece açık ve sağlam olan bir arayüzdür. Yönlendiriciye bağlı herhangi bir LAN kurulu olmasa da loopback arayüz sayesinde burada bir LAN varmış gibi yaptığımız yapılandırmaları test edebiliriz. 
 
 ### Loopback adresi ne demek?
Localhost arka planda 127.0.0.1 Ip Adresidir. Bilgisayarin kendisine TCP/IP üzerinde erismesini saglamak için loopback aygiti adi verilen sanal bir ag karti olusturularak giden veriler bu adrese yönlendirilir.

### GNS3 Lookback Interface Ekleme
 Fiziksel pc'den GNS3'teki bir routera bağlanmamız gerekiyor bu ve benzeri nedenlerden Loopback kurulumu yapmalıyız. 
##### Kurulum;
 - GNS3'nin alt klasöründe Loopback Manager yönetici olarak çalıştırılmalıdır.
   - ###### Bu kısımdan şunları yapabiliriz;
   - 1- Bu kısımdan mevcut olanları listeleyebiliriz.
   - 2- Yeni bir Loopback adaptör oluşturabiliriz (reboot gerektirir.)
   - 3- Mevcut bir interface'i kaldırabiliriz.
   - 4- Tüm interface'leri kaldırabiliriz.
   - 5- Pcyi reboot edebiliriz.
   - 6- Çıkış
- Yeni bir loopback oluşturacağımız için 2'yi seçiyoruz.
- Oluşturduğumuz loopback interface'in etkinleşmesi için bilgisayarı kapatıp açmamız (reboot) gerekiyor. Bunu kendinizde yapabilirsiniz 5. seçeneği de seçebilirsiniz.
- Denetim masası (Control Panel) --> Ağ ve İnternet (Network and Internet) --> Ağ ve Paylaşım Merkezi (Network and Sharing Centre) --> Bağdaştırıcı Ayarlarını Değiştirin (Change adapter settings) --> Ethernet tanımlanmayan ağ (Unidentified network) bu bizim oluşturduğumuz loopback bizim buna ip adresi atamamız gerekmektedir.
- Üzerinde sağ tıklayıp özellikleri açıyoruz. (Properties)
- TCP/IPv4 e tıklayıp ip atamasını yapıyoruz. Buradan static bir ip adresi verebiliriz. Örneğin;
 ![image](https://user-images.githubusercontent.com/45692102/127765481-ddeea883-659e-4b1b-84a9-44cbcd8b8786.png)
Bu şekilde loopback'i kullanabiliriz.
 
 
 ## Cisco Router Nedir, Nasıl Eklenir?
 Cisco router, IP paketlerini bir ağdan diğerine taşımaya yarayan cihazlara verilen isimdir, Türkçe ismi ile “yönlendirici” olarak bilinmektedir. Cisco Router ürünleri; ana kart, işlemci, ROM ve RAM'den oluşmaktadır. Cisco Router cihazlarının diğer ürünler ile iletişim kurabilmesi için ara yüzleri bulunur.
 -Setup Wizarddan son aşamaya geliyoruz
 ![image](https://user-images.githubusercontent.com/45692102/127766096-03ce7b53-5348-4eea-a134-0b0c5230a768.png)
![image](https://user-images.githubusercontent.com/45692102/127766116-1d05ffc0-f7fe-4380-85ed-49db8a999f7b.png)

![image](https://user-images.githubusercontent.com/45692102/127766136-e71d5fc4-93a3-4e73-882c-dea3d4302c82.png)

**Kayıtlı imaj yoksa burası bu şekilde boş gelir.**

c7200-adventerprisek9-mz.153-3.XB12.image download bu şekilde googledan bir image yükleyebilirsiniz.

Daha sonra bu şekilde gözükecektir.

![image](https://user-images.githubusercontent.com/45692102/127766293-d44122b0-91f5-48fa-b2b7-142e026aaf15.png)

![image](https://user-images.githubusercontent.com/45692102/127766335-a6a5568d-af15-47a0-9cb4-80ea4aca1743.png)

**Bu kısımdan isim verebilirsiniz** Next diyoruz.

![image](https://user-images.githubusercontent.com/45692102/127766360-768048b9-1a22-49b7-9d9d-14c7fd7769ff.png)

**Bu kısımda ne kadar ram ayıracağımızı seçiyoruz.**

![image](https://user-images.githubusercontent.com/45692102/127766412-3ee7f997-8051-47ca-a713-ecc6d7f722fa.png)

**Idle-Pc Finder'ı çalıştırıyoruz.**

En son finish'e basıyoruz ve artık işlemimiz tamamlanmış oluyor.

![image](https://user-images.githubusercontent.com/45692102/127766465-d0c789c5-a339-4a65-ae28-ff54dcc6228d.png)









