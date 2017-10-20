---
title: "Google Plus Comments Ekleme"
date: 2017-09-16T20:47:03+03:00
konular : ["web","hugo"]
tags: ["google","plus","comments"]
slug: "google-plus-comments-ekleme"
---


Web sitenize Google plus'a ait yorum eklentisini kurmak istiyorsunuz. Bencede haklısınız. Facebook Comments biraz hantal ve bazı firmalar facebook'a engel koyduğunda kişiler sitenizin açılışındaki yavaşlığın sitenizden kaynaklandığını düşünüşüp sitenizle ilgili olumsuz izlenimlere kapılacaklar.

Bu nedenle ben siteme Google Plus Comments eklemeyi tercih ediyorum. Nasıl mı ?

    <script src="https://apis.google.com/js/plusone.js"></script>
    <div id="comments"></div>
    <script>
    gapi.comments.render('comments', {
        href: window.location,
        width: '700',
        first_party_property: 'BLOGGER',
        view_type: 'FILTERED_POSTMOD'
    });
    </script>

Bu kadar da kolay :) 