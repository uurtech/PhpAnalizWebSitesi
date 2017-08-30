---
title: "Jquery ile Hugo Search Ekleme"
date: 2017-08-29T23:59:56+03:00
categories : ["jquery","hugo","firebase"]
tags: ["search","hugo","firebase"]
slug: "jquery-ile-firebase-siteye-search-ekleme"
---

Bildiğiniz gibi Google bize Firebase Hosting hizmetini verirken, sunucu taraflı bir script çalıştıramayağımızı da söylüyor. Neden ? Çünkü 2017 yılındayız, bu tür şeyler için API ve servis kodlanması gerekiyor. Ancak bizim micro işlerde bu kadar abartılı bir kullanıma ihtiyacımız yok. 

Ben bu sitede Hugo kullanıyorum, bu da verilerin kendi bilgisayarımda derlenip statik olarak Firebase'e yüklediğim anlamına geliyor. Peki Hugo ile yapılmış site de site içi aramayı nasıl eklerim ?

Basit, hugo bana zaten xml olarak site içeriklerimi veriyor, çünkü Google Search Console'a içeriklerimin gönderilmesi gerek. O zaman aklıma direk search'ü son kullancı tarafında bu XML dosyaları içerisinde yaptırabilirim yanıtı geliyor.

Bunun için temamdaki kütüphaneleri inceleyiyeyim,

        <script src="https://phpanaliz.com/js/jquery-1.11.3.min.js"></script>
        <script src="https://phpanaliz.com/js/jquery.fitvids.js"></script>

Yukarıda gördüğünüz gibi çoğu tema da olduğu gibi Jquery kullanılmış, o zaman hızlıca Jquery ile nasıl yapacağımıza bakalım.

Siteyi yayınladığım kodların içerisinde her verinin bulunduğu bir XML dosyası buldum,

    https://phpanaliz.com/index.xml

O zaman bu dosya üzerinde arama yaptırmalıyım, ilk olarak footer'a javascript kodlarımı ekliyorum, bu kodlar her seferinde çalışmasın sadece kelime aratılmışsa çalışsın diye de bir sorgu ekliyorum,

     
    <script type="text/javascript">
        function getParameterByName(name, url) {
        if (!url) url = window.location.href;
        name = name.replace(/[\[\]]/g, "\\$&");
        var regex = new RegExp("[?&]" + name + "(=([^&#]*)|&|#|$)"),
            results = regex.exec(url);
        if (!results) return null;
        if (!results[2]) return '';
        return decodeURIComponent(results[2].replace(/\+/g, " "));
    }
    var sonucSayac = 0;
    var string = getParameterByName("kelime");
    if(string !== null){
        var result = new Array();
       
                var feed = "/index.xml";
                    $.ajax(feed, {
                    accepts:{
                        xml:"application/rss+xml"
                    },
                    dataType:"xml",
                    success:function(data) {
                        
                        $(data).find("item").each(function () {
                            var el = $(this);
                                if(el.find("description").text().indexOf(string) > -1){
                                sonucSayac++;
                                $("#sonuclar").append('<li class="post-stub" itemprop="blogPost" itemscope="" itemtype="https://schema.org/BlogPosting"><a href="'+el.find("link").text()+'" itemprop="url" title="Detaylar"><h4 class="post-stub-title" itemprop="name">'+el.find("title").text()+'</h4></a></li>');    
                            }
                        });
                
    if(sonucSayac == 0){
                    $("#sonuclar").append('<li class="post-stub">Sonuç bulunamadı</li>');
                }
                    }   
                });
                
    }
            
    
            </script>

Bununla birlikte bir de input'a ihtiyaımız var, bu input'u header'da uygun gördüğüm bi yere ekliyorum, eklediğim arama formu şu şekilde

    <form id="search" method="get" action="/sayfa/search/">
                                <input type="text" name="kelime" id="kelime" placeholder="Arama"/>
                                </form>

Sonrasında komut satırından yeni bir sayfa oluşturmalıyım,
    hugo new sayfa/search.md

Bu oluşturduğum sayfaya ise sadece ul ekliyorum, 

    ---
    title: "Arama"
    date: 2017-08-30T14:21:07+03:00
    description: "Arama Sayfası"
    ---

    <ol class="post-list" id="sonuclar">

    </ol>

ve artık tamamlandı. Hugo sitemin bir arama motoru var ! :) 