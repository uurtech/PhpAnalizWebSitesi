---
title: "Php Komut Satırı Kodlari Çalıştırmak"
date: 2017-10-14T12:38:47+03:00
konular : ["php","komut satiri"]
tags: ["php","komut satiri"]
slug: "php-komut-satiri-kodlari-calistirmak"
---


***PHP*** ile kod yazarken bazı özel durumlarda işletim sisteminde bulunan scriptleri veya uygulamaları çalıştırmanız gerekebilir. PHP'de komut satırında işlem yapmamızı sağlayan bir kaç adet method bulunuyor.

Sıralayalım

* escapeshellarg — Bir komutun değiştirge dizgesini önceler
* escapeshellcmd — Kabuk meta karakterlerini önceler
* exec — Bir komut çalıştırır
* passthru — Harici bir programı çalıştırır ve çıktısını ham olarak gösterir
* proc_close — proc_open tarafından açılmış bir süreci kapatır ve sürecin çıkış kodunu döndürür
* proc_get_status — proc_open tarafından açılmış bir süreç hakkında bilgi döndürür
* proc_nice — Çalışan sürecin önceliğini değiştirir
* proc_open — Bir komutu çalıştırır ve G/Ç için bir dosya tanıtıcı açar
* proc_terminate — proc_open ile açılmış bir süreci öldürür
* shell_exec — Komutu kabukta çalıştırır ve çıktısının tamamını bir dizge olarak döndürür
* system — Belirtilen harici komutu çalıştırır ve çıktısını gösterir


Bunların arasında ***system*** fonksiyonu *C* dilinde de mevcut. Diğerleri ile ilgili emin değilim. Konumuza dönelim. 

Ek olarak bir adet daha yöntem var, direk mevcut komutu "echo" ile yazdırmak yani,

    $out = "dir /p";//veya ls (linux/mac için)
    echo $out;

Ancak bu komutun çalıştırılabilmesi için SadeMode'un kapatılması gerekiyor. Bence sırf böyle bir şey yapmak için buna gerek yok. 

Ben genellikle *exec()* veya *shell_exec()* methodlarını kullanıyorum.

*exec* methodunu bir işlemi işletim sistemine yaptırıp, dönen verilerden son satırı alacaksak (bazen gerçekten lazım oluyor) kullanıyoruz. Örneğin 
    $out = exec("dir /p");//veya ls (linux/mac için)
    echo $out;

Komutu ekrana basılan son satırı sizlere geri döndürecektir.

*shell_exec()* ise ne geri dönüyorsa sizlere onu getirecektir. 