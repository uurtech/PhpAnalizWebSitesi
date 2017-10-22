---
title: "Vhost Script Kullanımı"
date: 2017-08-28T23:14:26+03:00
konular : ["php","script"]
tags: ["php","github","script","vhost","vhost kullanımı","local domain"]
image: "/images/php-gelistir.jpg"
slug: "vhosts-script-kullanimi"
---

***MAMP, XAMPP veya WAMP*** ne kullandığınız aslında pek önemli değil, Apache üzerinde vhost kullanmak istiyorsanız, bu işi biraz pratikleştirmeniz gerekiyor. Ben kendi bilgisayarımda Komut Satırını kullanmayı sevdiğim için birazdan belirteceğim scripti şu şekilde kullanıyorum

    php vhosts.php
    DİZİN
    localDomain.dev

Bu parametreleri alarak tanımladığım vhosts dosyasında ve işletim sistemimdeki hosts dosyasındaki düzenlemeyi yaparak beni tekrar tekrar dosyalara girmekten kurtarıyor.

Şimdi yerel cihazda projeye özel yerel domain kullanmak için PHP kodumuzu inceleyelim

    <?php
    $i = 0;
    $infos = array();
    while($f = fgets(STDIN)){
        $i++;
        $infos[] = str_replace("\n","",$f);
        if($i == 2){
            break;
        }
    }
    if(count($infos) > 2) die("pls.");
    $string = '<VirtualHost *:80>
    ServerAdmin email@email.com
    DocumentRoot "C:/xampp/htdocs/'.$infos[0].'"
    ServerName '.$infos[1].'
    ServerAlias '.$infos[1].'
    </VirtualHost>
    ';
    $local_link = "127.0.0.1            ".$infos[1];
    file_put_contents("C:/xampp/apache/conf/extra/httpd-vhost.conf",$string,FILE_APPEND);
    file_put_contents("C:/Windows/System32/drivers/etc/hosts",$local_link,FILE_APPEND);
    ?>

Laravel projelerim için dizini belirtirken ***projeAdi/public*** diyerek yapabiliyorum. 
Bununla birlikte kullandığınız işletim sistemine göre, aşağıdaki iki satırı düzenleyin

    file_put_contents("C:/xampp/apache/conf/extra/httpd-vhost.conf",$string,FILE_APPEND);
    file_put_contents("C:/Windows/System32/drivers/etc/hosts",$local_link,FILE_APPEND);

Bunlarla birlikte Apache yapılandırma dosyanızda bu belirtilen vhosts dosyasının Include edildiğinden emin olun. 

Xampp için ***DISK\xampp\apache\conf\httpd.conf***
MAMP için ***DISK\MAMP\conf\apache\httpd.conf***
WAMPP için ***C:\wamp\bin\Apache2.4\conf\httpd.conf***

Dosyalarını açın ve içerisinde Vhosts diye aratın, 

    #Include conf/extra/httpd-vhosts.conf

benzer bir satır olacak (tabi ki işletim sisteminize ve kullandığınız pakete göre değişecektir), bu satırın başındaki # işaretini kaldırın ve XAMPP/MAMP/WAMP ne kullanıyorsanız, içerisindeki Apache'yi yeniden başlatın.

Bu script için Github Repo oluşturmaya gerek yoktu ancak, popüler programlama dilleri içinde benzer scriptler yazılabilir, Repo'ya gitmek için <a href="https://github.com/uurtech/vhosts-creator-script" target="_blank">https://github.com/uurtech/vhosts-creator-script</a> bağlantısını ziyaret edebilirsiniz.