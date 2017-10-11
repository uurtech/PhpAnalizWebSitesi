---
title: "Php ile Proxy Değiştirme"
date: 2017-10-11T10:25:13+03:00
categories : ["php"]
tags: ["proxy","php"]
slug: "php-ile-proxy-degistirme"
---


PHP uygulaması geliştirirken, özel nedenlerden dolayı proxy değiştirmeye ihtiyacınız olabilir, belki hile geliştiriceksiniz, belki de sisteminizi dış bağlantılarla kontrol edeceksiniz, belki de çok orijnal bir şey için ihtiyacınız var. PHP'de proxy değiştirmeye ihtiyacınız olduğunda çok rahat yapabiliyorsunuz. Önemli olan hangi metodla kendi PHP uygulamanıza uyarlamanız,

İlk örnek ***CURL*** ile PHP'de proxy değiştirme

    function getUrl($url)
    {
        $ch = curl_init(); 
        $timeout = 5; // set to zero for no timeout 
        curl_setopt ($ch, CURLOPT_CONNECTTIMEOUT, $timeout); 
        curl_setopt ($ch, CURLOPT_URL, $url); 
        curl_setopt ($ch, CURLOPT_RETURNTRANSFER, 1); 
        curl_setopt($ch, CURLOPT_PROXY, "http://proxy.example.com"); //proxy adresi
        curl_setopt($ch, CURLOPT_PROXYPORT, "8080"); // proxy portu
        curl_setopt($ch, CURLOPT_PROXYUSERPWD, "username:pass"); //kullanıcı adı ve şifre 
        $file_contents = curl_exec($ch); 
        curl_close($ch); 
        return $file_contents;
    }

    echo  getUrl("https://phpanaliz.com");


Ya da PEAR HTTP_Request2 modülü ile;

    function UrlOpen($url)
    {
    $request = new HTTP_Request2($url);

    $request->setConfig(array(
        'proxy_host' => '192.168.1.6',
        'proxy_port' => 8080,
        'proxy_user' => 'MYUSER',
        'proxy_password' => 'MYPASS',
        'ssl_verify_peer' => False,
        'connect_timeout' => 3,
    );

    return $request;
    }

    $req = UrlOpen($url);
    $res = $req->send();
    if ($res->getStatus() == '200')
    $data = $request->getBody();


PHP'de proxy değiştirip hem ***CURL***'de hem de ***file_get_contents*** ile kullanmak istiyorsanız

    stream_context_set_default(['http'=>['proxy'=>'proxy-host:proxy-port']]);

PHP ile uygulama geliştirmeyi o kadar seviyorum ki, neyse PHP ile Proxy değiştirme işlemi bu kadar rahat yapılıyor.