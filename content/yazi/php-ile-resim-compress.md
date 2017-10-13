---
title: "Php ile Resim Compress"
date: 2017-10-12T21:16:07+03:00
categories : ["php"]
tags: ["php","tinypng","api"]
slug: "php-ile-resim-dosya-boyutu-kucultme"
---


***PHP***'de geliştirdiğim bir scripti sizlerle paylaşmak istiyorum. Aslında çok basit küçük bir uygulama ama çok işime yarıyor.

Müşterilerimize web sitelerini verirken, tinypng üzerinden resim sıkıştırıp yayınlıyoruz, Tinypng'nin Photoshop eklentisi ise sadece Windows'ta çalıştığı için satın almamız bir şey ifade etmeyeceğinden, dizindeki resimleri sıkıştırıp başka bir klasöre atan bir script geliştirdim.

Scripti github üzerinden geliştirebilirsiniz [buradaki](https://github.com/uurtech/tinypng-php-compresser) adresten erişebilirsiniz.

İlk olarak [tinypng.com](http://tinypng.com) adresine girip ücretsiz developer key talep ediyoruz, şifre bile girmenize gerek yok, gelen e-posta ile login olup developer key'i alabilirsiniz.

Sonrasında composer ile Tinypng kütüphanesini projemize dahil ediyoruz.

    composer require tinify/tinify

Gerekli dosyalar indikten sonra php kodumuzu aşağıdaki gibi yazıyoruz

    require_once("vendor/autoload.php");
    \Tinify\setKey("YOUR_API_KEY");
    $images = glob('images/*.{jpeg,jpg,png}', GLOB_BRACE);
    var_dump($images);
    if (!file_exists('compressed')) {
        mkdir('compressed', 0777, true);
    }
    foreach($images as $image){
        $source = \Tinify\fromFile($image);
        $source->toFile(str_replace("images","compressed",$image));
    }

Bu scripti çalıştırdığınız dizinde images adlı klasördeki her resmi alıp sıkıştırıp compressed klasörüne atacaktır. Tinypng çok başarılı sıkıştırma işlemi yaparken ayda 500 adet kullanımı ücretsiz veriyor. 

Freelance işlerinizde kullanıp, site açılış performansını etkilyecek dosya boyutlarıyla müşterinizi etkliyebilirsiniz.

