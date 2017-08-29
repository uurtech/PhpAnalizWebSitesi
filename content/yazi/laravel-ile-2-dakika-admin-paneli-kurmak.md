---
title: "Laravel ile 2 Dakika Admin Paneli Kurmak"
date: 2017-08-29T22:27:45+03:00
categories : ["Laravel","Voyager","PHP"]
tags: ["laravel","php","voyager"]
image: "/images/laravel-voyager.jpg"
slug: "laravel-ile-2-dakikada-admin-paneli-kurmak"
---

Bu kurulumu yapmanın ne kadar sürdüğüne baktığımda 1.56 dakika olduğunu gördüm. Müşteriniz eğer internet üzerinden satın aldığınız arayüzlerden birini beğenirse bir kaç saatte komple sağlam bir CMS'e sahip siteyi sadece giydirme yaparak yayına alabilirsiniz.

Voyager'ın admin panelinden dinamik olarak Model ve Controller oluşturulabiliyor, bu sayede yetenekleri sınırsız. Kullanıcı yetkilendirme işlemi bile panelden rahatlıkla yapılabiliyor ve sizin hiç bir şey ayarlamanıza gerek kalmıyor. 

İlk olarak sinir olacağınız kadar kolay bir kullanımı mevcut, bilgisayarınız laravel kullanımına uygun değilse, hızlıca kurulumlara başlayalım, 
İlk olarak, ***XAMPP***, ***WAMP*** veya ***MAMP*** kurmalısınız, benim tavsiyem kesinlikle ***MAMP***. 

Bu programları kurarken herhangi bir ayarlamaya şuan ihtiyacımız olmadığı için kurulumu anlatmayı gerek duymuyorum. Bizim odak noktamız şuan ***Laravel*** ve başarılı bir yönetim paketi olan ***Voyager***

Laravel kurulumu için bir PHP geliştiricinin olmazsa olmazı ***Composer***'a da ihtiyacımız var, Eğer bilgisayarınızda dahili bir PHP versiyonu var ise, PATH ayarı yapmadan çalışacağından aşağıdaki komutlarla Composer'ı kurabilirsiniz,

    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
    php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
    php composer-setup.php
    php -r "unlink('composer-setup.php');"

Örneğin Mac cihazımda her zaman PHP mevcut idi. Devam edelim, 

_Buraya kadar herhangi bir sorun yaşadıysanız lütfen yaşadığınız sorunu paylaşın hızlıca çözümleyelim._

Komut Satırımızı açıyoruz, 

    composer create-project laravel/laravel ProjeAdi "5.3.*"

Burada fark ettiğiniz üzere Laravel'in 5.3 sürümünü tercih ettik, sebebi ise, Voyager şuan en sorunsuz şekilde Laravel 5.3'te çalışıyor.

Laravel kurulumunu yaptıktan sonra, _.env_ dosyamıza girip, MysQL bağlantılarımızı yapıyoruz

    DB_HOST=localhost
    DB_DATABASE=veritabanı
    DB_USERNAME=kullanıcı
    DB_PASSWORD=şifre

Bu aşamadan önce mutlaka veritabanınızı PhpMyAdmin üzerinden oluşturmuş olmalısınız. 

Laravel kurulumu çalıştıktan sonra _localhost/ProjeAdi/public_ adresine erişimimiz sorunsuz olmalı. Yerel cihazınızda Domain kullanımı için vhost kullanımını [burada](https://phpanaliz.com/yazi/vhosts-script-kullanimi/) bulabilirsiniz.

Tekrar komut satırımıza geri dönüyoruz, projemizin dizinine giriyoruz 

    cd ProjeAdi
    composer require tcg/voyager

Şimdi, Laravel'imizin Voyager'ı tanıyabilmesini sağlayalım, _Config->app.php_ içerisine Provider ekliyoruz,

    'providers' => [
        // Buralar Laravel'in kendi sağlayıcı sınıfları

        
        TCG\Voyager\VoyagerServiceProvider::class,
       

        // Buradan itibaren de servis sağlayıcı sınıflar
    ],

Artık hazırız, yapmamız gereken komut satırından proje dizinine gelip kurulumu başlatmak, dilerseniz Dummy Data ile de kurulum yapabilirsiniz, ancak ben tertemiz bir kurulumu tercih ediyorum,

    php artisan voyager:install

    //eğer dummy data isterseniz,
    php artisan voyager:install --with-dummy

Kurulumu yaptıktan sonra admin eklemeniz gerekiyor,

    php artisan voyager:admin your@email.com --create

Evet artık kuruldu, _localhost/ProjeAdi/public/admin_ veya _localhost/ProjeAdi/public/index.php/admin_ üzerinden erişim sağlayabilirsiniz. Buradaki index.php'nin eklenmesi kuracağınız Apache2 paketinin varsayılan ayarlarından kaynaklanıyor. 

Sizlere tavsiyem [vhosts](https://phpanaliz.com/yazi/vhosts-script-kullanimi/) ile yerel domain kullanmanız.


