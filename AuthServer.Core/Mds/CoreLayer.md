## Hangi Entityler Olacak?
UserRefreshToken,UserApp ve Product adinda 3 entity olacak.
UserApp, IdentityUser classindan miras alacak.
UserRefreshToken
Genelde AuthServerda butun controlleri tutuyoruz. Hem controlleri hemde icerisindeki datalardan ilgili datalari donuyor.(Kisisel proje)
Sirket icin sadece token isini yapar authserver.