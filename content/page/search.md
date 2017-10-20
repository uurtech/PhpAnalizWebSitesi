---
title: "Arama"
date: 2017-08-30T14:21:07+03:00
description: "Arama Sayfası"
---

<ol class="post-list" id="sonuclar">

</ol>

<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js" type="text/javascript"></script>

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