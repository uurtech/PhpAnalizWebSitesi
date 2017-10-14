---
title: "Php ile Terminalde Emoji Yazdırmak"
date: 2017-10-14T15:30:58+03:00
categories : ["php","emoji","bash"]
tags: ["php","bash","terminal","emoji"]
slug: "php-ile-terminalde-emoji-yazdirmak"
---


***PHP*** ile konsola [komut gönderimine](https://phpanaliz.com/yazi/php-komut-satiri-kodlari-calistirmak/) bakmıştık, bu sefer konsol üzerinde emoji yazdırmaya bakalım.

Nerden aklına geldi derseniz, forumlarda baya baya sormuş arkadaşlar, bulunsun istedim.

Tahmin ettiğiniz gibi yapmamız gereken PHP'de komut satırına "bu işi sen yap" demek. 

Şimdi mevcut sistem üzerindeki komutu çalıştırması için *system()* methodunu kullanarak emojiyi yazdırmasını sağlayacağız.

    system("echo \xE2\x98\xA0");

Gördüğünüz gibi, terminalde ekrana yazı yazdırma komutumuz echo, bu windows tarafında da bu şekilde. 

Peki buradaki bu karakterler ne anlama geliyor. UTF8 6 byte olarak emojinin kodunu belirtiyoruz, bizim için bunu konsol yorumluyor. Enter tuşunun 13 numaralı key'i döndürmesi gibi düşünün.

Ezbere yazmak sizleri uğraştırabilir :) 

[bu adreste](https://apps.timwhitlock.info/emoji/tables/unicode) emojilerin Unicode ve Byte hali bulunuyor.

Byteları incelerseniz, kategorize edip bir diziye atıp algoritmik olarak emojileri oluşturabilirsiniz.
