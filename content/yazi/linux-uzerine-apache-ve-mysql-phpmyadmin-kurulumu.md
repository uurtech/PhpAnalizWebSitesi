---
title: "Linux Üzerine Apache,Mysql ve Phpmyadmin Kurulumu"
date: 2017-10-20T11:16:55+03:00
konular : ["linux","ubuntu","apache","mysql","phpmyadmin"]
tags: ["Linux","ubuntu","apache","mysql","phpmyadmin"]
slug: "linux-uzerine-apache-mysql-phpmyadmin-kurulumu"
---


***Linux*** üzerine sistem üzerine ***Apache, MySQL ve Phpmyadmin*** kurulumu yapıp test edicez. 

Hızlıca başlayalım, ssh üzerinden linux sunucumuza bağlanıyoruz.

    ssh root@IP_ADRESİ

Çıkan ekranda şifrenizi girin (korkmayın klavyeye girince ekranda hiç bir hareket olmaz, girip Enter'a basın).

Sonrasında hızlıca bir update yapalım

    sudo apt-get update

Şimdi Apache'mizi indirip kuralım

    sudo apt-get install apache2

Çıkan soruya Y veya E diye yanıtlayıp Enter'a basıyoruz.

kurulumu tamamladık, şimdi bakalım Apache2'miz çalışıyor mu ? 

Favori tarayıcınızı açın (tabi ki ***Google Chrome***) ve sunucu ***IP*** adresini yazın, karşıma şu çılgın ekran gelecek

<img src="/images/apache2-hosgeldin-ekrani.png" alt="apache2 kurulumu" />

Apache'nin ayarlarına şimdilik dokunmuyor ve hemen MySQL kurulumuna geçiyoruz,

    sudo apt-get install mysql-server

MySQL kurulumu yapılırken sizlerden Root şifresi isteyecek, ergenlerin sızamayacağı bir şifre girerseniz sadece işinde uzmanların sızabileceği ancak eziklerden uzak bir MySQL şifreniz olur.

MySQL'e de dokunmuyoruz :), şimdi Apache için gerekli php ile birlikte php'nin apache ve mysql modüllerini kuralım

    sudo apt-get install php libapache2-mod-php php-mcrypt php-mysql

Burada kurduğumuz php versiyonu ***7*** oluyor. Çünkü Linux dağıtımlarında artık php direk 7. sürümü çağırıyor.

Sırada hayat kurtarıcı ***PhpMyAdmin***

    sudo apt-get install phpmyadmin php-mbstring php-gettext

PhpMyAdmin kurulumu sırasında da bizlere hangi web uygulamasını kullanacağımızı soruyor.Apache'yi seçtikten sonrasında PhpMyAdmin kendi ihtiyacı olan veritabanını kurmak için onay ve ardından şifre isteyecek, MySQL şifrenizi çekinmeden girin.

PhpMyAdmin için aktif etmemiz gereken iki adet php modülü mevcut

    sudo phpenmod mcrypt
    sudo phpenmod mbstring

Evet artık son bir adım kaldı. PhpMyAdmin'i tanıtmak ve aktifleştirmek

    sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf
    sudo a2enconf phpmyadmin
    sudo service apache2 reload

Son komutumuz ile apache baştan başlatılacak ve artık ip/phpmyadmin adresinden erişebileceksiniz.
