---
title: "Hugo Datetime Degistirme"
date: 2017-07-09T20:47:25+03:00
description: "Hugo'ya Google Analytics Kodu Ekleme"
tags: [ "hugo", "datetime", "Go Lang"]
date: "2017-07-09"
categories:
  - "Hugo"
  - "Go Lang"
slug: "hugo-datetime-degistirme"
image: "/images/hugo.jpg"
Description: "Hugo Datetime Değiştirme"
---

Bilmiyorsanız hemen söyliyeyim, Hugo, **Go Lang** ile geliştirilmiş bir tool, web sitesinin **gohugo** olması buradan geliyor.
Hugo sistemini kurduğunuzda tema da gözünüze batan ilk şeylerden biri, tarihlerin amerikan stili olması, çünkü alışık değiliz !

Tema üzerinde **.Site.Params.DateForm** gibi bir tanımlama var ise, config dosyanızdan, yok ise doğrudan oraya da yazabilirsiniz. 
İlk olarak Config dosyasına DateForm diye bir değişken tanımlayalım,

<pre><code>
baseURL = "https://mobilsihirbazi.com/"
languageCode = "tr-TR"
title = "Mobil Sihirbazı - ios ve android"
theme = "hugo_theme_robust"
Description = "Mobil Sihirbazı, ios ve android üzerine."
DefaultContentLanguage = "tr"

[params]
	DateForm = "02/01/2006"
</code></pre>

buradaki 02, go lang içerisinde günü, 01 ise ayı temsil ediyor.Bu tanımlamadan sonra aşağıdaki gibi temanıza çağırabilirsiniz,
<pre><code>
{{ with .Site.Params.DateForm }}{{ $.Date.Format . }} {{ end }}
</code></pre>

Eğer direk temanızın içerisine yazmak isterseniz, 

<pre><code>
{{ $.Date.Format "02/01/2006" }}
</code></pre>

Şeklinde de yapabilirsiniz. 