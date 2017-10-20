---
title: "Cloudflare Jquery Sorunu"
date: 2017-10-18T07:23:26+03:00
konular: ["cloudflare","jquery"]
tags: ["jquery","cloudflare","çözüm","construct 2"]
slug: "cloudflare-jquery-sorunu"
---


Construct 2 ile oyun geliştirdik, Cloudflare premium hesabını mevcut adresimize yönlendirdik ancak Safari haricindeki tarayıcılarda oyun çalışmıyordu.

Saatlerce oyun ile ilgili sorun olduğunu düşündükten sonra sorunun cache ile ilgili olduğunu tespit edip bu yönde çalışmaya başladık. Oyun sayfamızdaki elementlerin sorunsuz yüklenmesi ve Safari'de çalışmasının sonunda, oyunu çağıran kodlarımıza bir bakmak istedik ve gördük ki, document.ready fonksiyonu çalıştırılmıyor ancak bu konuda herhangi bir hatanın konsolda olmaması bizlere bu zamanı kaybettirdi. 

Dikkatimize çarpan şey ise jquery'nin sayfa içerisine alınırken tipinin değiştirilmesi yani şu şekilde,

    <script type="jquery.js" type="text/rocketscript"></script>
Şeklinde çağırılıyor, oyunu export ederken bu şekilde bir dönüşüm olmadığını görünce cloudflare'in bu işi yaptığını düşünüp panele girdiğimizde gördük ki Rocket özelliği ile kendisi javascript css ve html'i revize ediyor. 

Bu özelliği kapatıp cloudflare üzerindeki cache'i sildikten sonra sorunumuz ortadan kalktı, bu sayede Construct 2 ile geliştirdiğimiz oyun artık çalışıyor.

