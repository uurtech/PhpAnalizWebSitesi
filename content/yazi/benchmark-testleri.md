---
title: "Benchmark Testleri"
date: 2017-09-21T01:24:43+03:00
categories : ["Kitap","benchmark","php"]
tags: ["php","benchmark","kitap"]
slug: "benchmark-testleri"
---

Bu yazıda PHP'i şu dili böyle döver falan gibi saçma şeyler olmayacak, her yazılım dilinin başka bir dile üstün olduğu alanlar mevcuttur ki 2017 yılında Cache sistemlerinin olması nedeniyle doğru yapılan işlerde dillerin pek önemi kalmıyor. Biz benchmark testlerine bakıp PHP'nin performans olarak ileride olduğu noktaları inceleyelim,

İlk olarak, Script dilleri ile ilgili karşılaştırmasına bakalım

***Mandelbrot fractal***'ı kaç saniye de render'lıyorlar bakalım,

* PHP : 0.281
* Ruby : 0.684
* Python : 1.128
* Perl : 2.083

İlk aşamada görüldüğü üzere PHP artisliğini yapıyor. PHP7'nin bu kadar hızlanmasındaki en büyük etkenlerden biri Intel'in performans takımının PHP7'nin geliştirilmesine danışmanlık yapmış olması.

Biraz daha detaylanalım,

<table>
      <tbody>
      <tr>
        <th colspan="3"><a href="https://benchmarksgame.alioth.debian.org/u64q/spectralnorm.html"><span>spectral-norm</span></a>
        </th><th colspan="3">
      </th></tr><tr>
        <th>source
        </th><th>secs
        </th><th>mem
        </th><th>gz
        </th><th>cpu
        </th><th>cpu load
      </th></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=spectralnorm&amp;lang=php&amp;id=1"><span>PHP</span></a>
        </td><td class="best">37.94
        </td><td>19,420
        </td><td>1135
        </td><td>150.67
        </td><td class="message">99%&nbsp;99%&nbsp;100%&nbsp;99%
      </td></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=spectralnorm&amp;lang=python3&amp;id=5"><span>Python&nbsp;3</span></a>
        </td><td>188.83
        </td><td>54,524
        </td><td>437
        </td><td>750.46
        </td><td class="message">99%&nbsp;100%&nbsp;100%&nbsp;99%
      </td></tr></tbody><tbody>
      <tr>
        <th colspan="3"><a href="https://benchmarksgame.alioth.debian.org/u64q/regexredux.html"><span>regex-redux</span></a>
        </th><th colspan="3">
      </th></tr><tr>
        <th>source
        </th><th>secs
        </th><th>mem
        </th><th>gz
        </th><th>cpu
        </th><th>cpu load
      </th></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=regexredux&amp;lang=php&amp;id=1"><span>PHP</span></a>
        </td><td class="best">3.34
        </td><td>158,792
        </td><td>786
        </td><td>3.30
        </td><td class="message">25%&nbsp;26%&nbsp;22%&nbsp;92%
      </td></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=regexredux&amp;lang=python3&amp;id=1"><span>Python&nbsp;3</span></a>
        </td><td>14.86
        </td><td>439,208
        </td><td>486
        </td><td>27.92
        </td><td class="message">46%&nbsp;77%&nbsp;35%&nbsp;31%
      </td></tr></tbody><tbody>
      <tr>
        <th colspan="3"><a href="https://benchmarksgame.alioth.debian.org/u64q/nbody.html"><span>n-body</span></a>
        </th><th colspan="3">
      </th></tr><tr>
        <th>source
        </th><th>secs
        </th><th>mem
        </th><th>gz
        </th><th>cpu
        </th><th>cpu load
      </th></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=nbody&amp;lang=php&amp;id=3"><span>PHP</span></a>
        </td><td class="best">358.21
        </td><td>8,668
        </td><td>1082
        </td><td>358.12
        </td><td class="message">17%&nbsp;0%&nbsp;1%&nbsp;83%
      </td></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=nbody&amp;lang=python3&amp;id=1"><span>Python&nbsp;3</span></a>
        </td><td>787.02
        </td><td>7,744
        </td><td>1181
        </td><td>786.82
        </td><td class="message">0%&nbsp;1%&nbsp;0%&nbsp;100%
      </td></tr></tbody><tbody>
     <tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=mandelbrot&amp;lang=php&amp;id=3"><span>PHP</span></a>
        </td><td class="best">125.17
        </td><td>136,776
        </td><td>863
        </td><td>499.16
        </td><td class="message">100%&nbsp;100%&nbsp;100%&nbsp;100%
      </td></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=mandelbrot&amp;lang=python3&amp;id=7"><span>Python&nbsp;3</span></a>
        </td><td>273.43
        </td><td>53,416
        </td><td>686
        </td><td>1,091.35
        </td><td class="message">100%&nbsp;100%&nbsp;100%&nbsp;100%
      </td></tr></tbody><tbody>
      <tr>
        <th colspan="3"><a href="https://benchmarksgame.alioth.debian.org/u64q/knucleotide.html"><span>k-nucleotide</span></a>
        </th><th colspan="3">
      </th></tr><tr>
        <th>source
        </th><th>secs
        </th><th>mem
        </th><th>gz
        </th><th>cpu
        </th><th>cpu load
      </th></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=knucleotide&amp;lang=php&amp;id=4"><span>PHP</span></a>
        </td><td class="best">43.96
        </td><td>235,632
        </td><td>1060
        </td><td>142.28
        </td><td class="message">87%&nbsp;100%&nbsp;71%&nbsp;72%
      </td></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=knucleotide&amp;lang=python3&amp;id=3"><span>Python&nbsp;3</span></a>
        </td><td>84.73
        </td><td>221,028
        </td><td>1937
        </td><td>276.97
        </td><td class="message">97%&nbsp;93%&nbsp;91%&nbsp;91%
      </td></tr></tbody><tbody>
      <tr>
        <th colspan="3"><a href="https://benchmarksgame.alioth.debian.org/u64q/fasta.html"><span>fasta</span></a>
        </th><th colspan="3">
      </th></tr><tr>
        <th>source
        </th><th>secs
        </th><th>mem
        </th><th>gz
        </th><th>cpu
        </th><th>cpu load
      </th></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=fasta&amp;lang=php&amp;id=3"><span>PHP</span></a>
        </td><td class="best">59.37
        </td><td>8,896
        </td><td>1030
        </td><td>59.36
        </td><td class="message">5%&nbsp;2%&nbsp;3%&nbsp;100%
      </td></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=fasta&amp;lang=python3&amp;id=3"><span>Python&nbsp;3</span></a>
        </td><td>110.91
        </td><td>8,024
        </td><td>977
        </td><td>110.87
        </td><td class="message">100%&nbsp;1%&nbsp;1%&nbsp;1%
      </td></tr></tbody><tbody>
      <tr>
        <th colspan="3"><a href="https://benchmarksgame.alioth.debian.org/u64q/fannkuchredux.html"><span>fannkuch-redux</span></a>
        </th><th colspan="3">
      </th></tr><tr>
        <th>source
        </th><th>secs
        </th><th>mem
        </th><th>gz
        </th><th>cpu
        </th><th>cpu load
      </th></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=fannkuchredux&amp;lang=php&amp;id=3"><span>PHP</span></a>
        </td><td class="best">280.04
        </td><td>33,588
        </td><td>1150
        </td><td>1,117.48
        </td><td class="message">100%&nbsp;100%&nbsp;100%&nbsp;100%
      </td></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=fannkuchredux&amp;lang=python3&amp;id=4"><span>Python&nbsp;3</span></a>
        </td><td>483.79
        </td><td>51,896
        </td><td>944
        </td><td>1,880.10
        </td><td class="message">97%&nbsp;94%&nbsp;100%&nbsp;99%
      </td></tr></tbody><tbody>
      <tr>
        <th colspan="3"><a href="https://benchmarksgame.alioth.debian.org/u64q/pidigits.html"><span>pidigits</span></a>
        </th><th colspan="3">
      </th></tr><tr>
        <th>source
        </th><th>secs
        </th><th>mem
        </th><th>gz
        </th><th>cpu
        </th><th>cpu load
      </th></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=pidigits&amp;lang=php&amp;id=5"><span>PHP</span></a>
        </td><td class="best">2.15
        </td><td>9,884
        </td><td>394
        </td><td>2.15
        </td><td class="message">1%&nbsp;0%&nbsp;100%&nbsp;1%
      </td></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=pidigits&amp;lang=python3&amp;id=2"><span>Python&nbsp;3</span></a>
        </td><td>3.51
        </td><td>10,344
        </td><td>382
        </td><td>3.50
        </td><td class="message">0%&nbsp;2%&nbsp;1%&nbsp;100%
      </td></tr></tbody><tbody>
      <tr>
        <th colspan="3"><a href="https://benchmarksgame.alioth.debian.org/u64q/revcomp.html"><span>reverse-complement</span></a>
        </th><th colspan="3">
      </th></tr><tr>
        <th>source
        </th><th>secs
        </th><th>mem
        </th><th>gz
        </th><th>cpu
        </th><th>cpu load
      </th></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=revcomp&amp;lang=php&amp;id=3"><span>PHP</span></a>
        </td><td class="best">2.81
        </td><td>135,124
        </td><td>426
        </td><td>1.75
        </td><td class="message">31%&nbsp;21%&nbsp;44%&nbsp;57%
      </td></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=revcomp&amp;lang=python3&amp;id=6"><span>Python&nbsp;3</span></a>
        </td><td>2.82
        </td><td>265,428
        </td><td>800
        </td><td>4.18
        </td><td class="message">46%&nbsp;32%&nbsp;20%&nbsp;54%
      </td></tr></tbody><tbody>
      <tr>
        <th colspan="3"><a href="https://benchmarksgame.alioth.debian.org/u64q/binarytrees.html"><span>binary-trees</span></a>
        </th><th colspan="3">
      </th></tr><tr>
        <th>source
        </th><th>secs
        </th><th>mem
        </th><th>gz
        </th><th>cpu
        </th><th>cpu load
      </th></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=binarytrees&amp;lang=php&amp;id=5"><span>PHP</span></a>
        </td><td>88.07
        </td><td>736,372
        </td><td>1027
        </td><td>247.49
        </td><td class="message">92%&nbsp;77%&nbsp;23%&nbsp;91%
      </td></tr><tr>
        <td><a href="https://benchmarksgame.alioth.debian.org/u64q/program.php?test=binarytrees&amp;lang=python3&amp;id=1"><span>Python&nbsp;3</span></a>
        </td><td>86.90
        </td><td>451,548
        </td><td>581
        </td><td>306.31
        </td><td class="message">89%&nbsp;97%&nbsp;87%&nbsp;89%
      </td></tr></tbody><tbody>
     </tbody></table>

Sistem özelliklerimiz ise ;

    ***PHP***
    PHP 7.1.4 (cli) (built: Apr 16 2017 16:17:54) ( NTS )
    Copyright (c) 1997-2017 The PHP Group
    Zend Engine v3.1.0, Copyright (c) 1998-2017 Zend Technologies

    ***Python 3***
    Python 3.6.1 (default, Apr 18 2017, 10:33:41)
    [GCC 6.3.0 20170406]
    --enable-optimizations --with-lto
    make profile-opt

Bu yazı sizleri çok etkilemesin, PHP'nin popülerite olarak en yakını Python olarak görüldüğü için araştırmacılar buna ağırlık vermiş. Bir inceleme olması nedeniyle paylaşıyorum, unutmayı nönemli olan dilin popisi veya bir iki micro saniyelik farkları değil seçtiğiniz dili iyi bilmenizdir.