## Notlarim
Apiden datalari almiyorsak, kimlik dogrulama ve yetkilendirme islemleri cookie bazli yapiliyor.
Direk controller uzerinden action uzerinden datalari alirsa cookie bazli kimlik dogrulama yapiyoruz.
KIMLIK DOGRULama kullanici adi ve sifre ile var mi yok mu bakilan islemdir. Yetkilendirme ise kullaniciya hangi islemleri yapabilecegini belirler.
## Token
String bir ifade ama anlamli bir ifade.
Spa ve mobil uygulamalar iclerinde datayi gosterebilmesi icin bir api ihtiyaca duyar. Kimlik dogrulama ve kimlik yetkilendirme islemlerine ihtiyac duyalr.
## Web api uygulamasi tasarimi
Katmanli, kendisine ait bir veritabani olacak.
Kullanci uyelik sistemi ile ilgili tablolar olacak.
Identity api kutuphanesi kullanilacak.
Bu uygulamanin gorevlerinden birisi token dagitmak olacak.
Auth server tokenlari web uygulamasina verecek ondan sonra apilara istekleri gerceklestirecekler.
3 tane apimiz var senaryoda. Kendisine ait datatableslari var. 
Birde ayrica token dagitan authserver da diye bir api olacak. Katmanli mimari olacak.
## Tokeni neye göre dagitacagiz?
Web spa apiye istek yapmak icin auth serverdan token alacak. Kullanici adi ve password ile authserverda tutuyoruz ve oradaki veritabaninda saklayacagiz.
Email ve sifre girdiginde arka tarafta biz bunu authservera gonderiyoruz.
Eger bu email ve sifre veri tabaninda varsa bir token kaydediyoruz. 
Artik elimizdeki token ile apilara istek yapabilirzi. Bu string bir ifade icerisinde data tasiyabiliyoruz. Hangi apilara istek yapacagi bulunduracak.
Kullanicinin id, email, rolleri, hangi apilara istek yapacagina dair bilgileri bulundarabiliriz.
Kullanicinin sifresini tutmayacagiz tokenda. Kritik bilgileri tutmayacagiz.
Diger apilar ne bekliyorlar bir sitek yapildiginda yapilan requestin headerinda bir token bekliyorlar.
Tokenda sikinti varsa 401 donecegiz.
## Uyelik sistemi olmayan apida kontrol sistemini nasil kuracagiz?
Client id ve client secret  ile  alan tanimliyoruz. 
Clinet ve secret ile Auth servara istek ayiyoruz. Eger bunlar varsa yani bu clienti tanimlayacak username ve password var ise Web spaya geri donduyoruz.
Bu tokenda sadece hangi apiya istek yapacagini bildiren data var.
## Auth server hem token hem de ayri bir islem yaparsa?
Yani diyelim hem token dagitacak hem stock ile bir controlleri var.
Once token icin istek yapiyoruz. Eger token dogru ise stock controllerina ayni api icinde istek atiyoruz.
Gercek hayatta bu karsimiza cikabilir. Ama bu best practice degildir.
# Jwt nedir?
jsonun headerinda algoritma ve tip biligsi var.
Payload ise json oldugu icin url uzerinden gonderilebiliyor. Bu nedenle base64 ile encode ediyoruz. Cerez kullanma zorunlulugunu ortadan kaldiriyor.
Hizli bir sekilde dogrulama yapabiliyoruz.
Eger bir token kullanici icin olusturulmussa sub kismi kullanici id sini tutuyor.
3.kisim ise imza. Simetrik imzalama ve asimetrik imzalamadir.
Token imzaladim diyelim yani sifreledim Eger buradaki string ile imzalayip bir de dogruluyorsam buna simetrik denir.
Asimetrikte ise private ve public key vardir. Private key ile imzalanir public key ile dogrulanir. Public key herkesin elinde olabilir. Private key ise sadece imzalayanin elinde olur.
Api token verirken private key ile imzaliyor. Bu end pointte public keyi yayinliyor.
Private key ile imzaladiktan sonra client apilara istek yapiyor.
Api auth serverin public keyini alip imzayi dogruluyor. Eger imza dogru ise tokeni kabul ediyor.
3 tane farkli renk var 3 tane farkli seyden olusuyor.
## JWT HEADER
Kirmizi olan kisimdir.
Algoritma ve tip bilgisini tutar. Algoritma imzalama algoritmasini belirtir. Tip ise token tipini belirtir.
## JWT PAYLOAD
Mor renklidir.
Json olarak tutabilecegimiz datalar vardir.
Url olarak tasiyabiliriz. Bu nedenle base64 ile encode ediyoruz.
Cerez kullanma zorunlulugunu ortadan kaldiriyor.
Hizli bir sekilde dogrulama yapabiliyoruz.
Payloadda tutugumz datalar birer claimdir. Claimler key value seklindedir. Key claimin adini value ise claimin degerini tutar.

## JWT SIGNATURE
Imza kismini tutar. Simetrik imzalama ve asimetrik imzalamadir.
## Simetrik imzalama
String bir ifade ile imzalama ve dogrulama yapariz. Eger buradaki string ile imzalayip bir de dogruluyorsam buna simetrik denir.
Auth Server token verirken private key ile imzaliyor. Bu end pointte public keyi yayinliyor.bu asimetriktir.
Eger ikisi de ayni key ile imzaliyor ve dogruluyorsa buna simetrik denir. Public key herkesin elinde olabilir. Private key ise sadece imzalayanin elinde olur.
## Tokenin Guvenligi
Suresini belirtebilirim.
Tokenin icerisinde degisiklik yapamaz ama icerigi gorebilir.
## Access Token
buyuk bir ihtimalle jwt tokendir.
Apiya istek yaparken headerda bu tokeni gonderiyoruz. Tokenin icerisinde kullaniciya dair bilgiler var. Tokenin icerigini gorebiliriz ama tokeni degistiremeyiz.
Refreh token access tokenin omru bittigi almak icin kullandigim degerdir.
Refresh tokenin tipi hersey olabilir. Unik olmasi yeterlidir.
Access tokenin omru kisa refresh tokenin omru uzun olur. Refresh tokeni kullaniciya gonderiyoruz. Kullanici access tokeni refresh token ile degistiriyor.
Auth servera geldi. Auth server access ve refresht tokenina clienta gonderdi.
Local storagea kaydettim. 
Apilar hem tokenin omru hemde imzasini kontrol ediyor. Suresi bittiyse 401 donecek.
Eger refresh token varsa hic kullanicya haber vermeden auth servera bir istek yapiyoruz. 
Eger auth server refresh tokeni dogrularsa yeni bir access token veriyor.
Hem access hem refresh token omru biterse kullaniciyi login ekranina gonderiyoruz.
Refresh tokeni databasete kaydedecegiz ve omru de kaydecegiz.
Access tokeni veri tabaninda tutamayiz.

