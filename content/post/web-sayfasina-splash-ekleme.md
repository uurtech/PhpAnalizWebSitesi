---
title: "Web Sayfasına Splash Ekleme"
date: 2017-09-13T23:39:06+03:00
konular : ["Chrome","Web"]
tags: ["web","chrome","splash"]
slug: "web-sayfasina-splash-screen-ekleme"
---


Chrome'un 2 yıl önce getirdiği bir özellik, yerel web master sitelerinde bu özelliği görmedim. Google'ın Chrome paylaşımlarını incelerken dikkatimi çekti. Chrome kullanan kişiler web sitenizde splash screen görüp sitenize öyle geliyor, sanki uygulamaymış gibi.

Desktop'ta manası olmadığı için bu size mobilde bir kalite katıyor. Müşterilerinizin sitesine değil de kendi sitenize kalite katmayı tercih edebilirsiniz. 

Gelelim Web sitemize splash ekranı eklemeye,

İlk manifest dosyası oluşturuyoruz, dosyanın adı pek önemli değil ancak, html içerisinde geliştirinin bakarken ne olduğunu anlamasına adına adının manifest olması mantık :) 

dosyamız ***manifest.json***

    {
    "short_name": "Bu nasıl site yarabbim",
    "name": "İnanılmaz web sitem ++",
    "icons": [
        {
        "src": "launcher-icon-2x.png",
        "sizes": "96x96",
        "type": "image/png"
        },
        {
        "src": "launcher-icon-3x.png",
        "sizes": "144x144",
        "type": "image/png"
        },
        {
        "src": "launcher-icon-4x.png",
        "sizes": "192x192",
        "type": "image/png"
        }
    ],
    "start_url": "/index.html",
    "display": "standalone",
    "orientation": "landscape"
    }


Ardından html dosyamıza gelip bu manifest dosyasını tanımlıyoruz ki, Chrome bulup işleyebilsin,

    <link rel="manifest" href="/manifest.json">

Ek olarak bu splash screen özelliği Firefox ve Opera'da da bir yıldır destekleniyor,[edge](https://developer.microsoft.com/en-us/microsoft-edge/platform/status/webapplicationmanifest/) ise hala geliştirme sürecinde.

kısaca önümüzdeki yıllarda her tarayıcıya gelecek.

Kolay gelsin :) 