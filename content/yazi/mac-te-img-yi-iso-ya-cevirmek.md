---
title: "Mac'te img'yi iso formatına çevirmek"
date: 2017-09-22T23:16:45+03:00
konular : ["mac"]
tags: ["iso","img","ccd2iso"]
slug: "img-to-iso-mac"
---


***MacOS*** kullanırken bazı durumlarda acil terminal araçlarına ihtiyaç olabiliyor. Ben sanallaştırma yaparken, indirdiğim img dosyasını acilen iso'ya çevirme ihtiyacı hissettim, dahili olan araçlarla yaptığımda paket hataları vb. ile karşılaştım, araştırdığımda ise kullananların memnun kaldığı bir araç ile karşılaştım; ***CCD2iso***.

Bu aracı img dosyamı iso yapmak için kullandım ve, kesinlikle başarılı ve bir o kadar da hızlı.

Hemen ccd2iso'nun kurulumuna geçelim,

***terminal***i açıyoruz. Eğer ***brew*** sizlerde kurulu ise, direk ikinci komuta geçebilirsiniz.

    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null


    brew install ccd2iso


Nasıl kullanacağımıza gelince, aslında help'i direk anlatmış (ben web sitesine dönmeye üşenip direk help'e bakmıştım)

Çok basit

       ccd2iso [ILKDOSYA.IMG] [CIKAN.ISO]

Bu paketi linux üzerinde de kurabilirsiniz, windows için kullanmak isteyen arkadaşlar SourceForge sayfasındaki kaynak kodları indirip derleyebilirler (bir win kullanıcısının daha önce bunu yaptığını görmedim).