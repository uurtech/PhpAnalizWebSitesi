---
title: "Php Facebook Login Yeni Api"
date: 2017-10-14T13:33:21+03:00
categories : ["php","social sdk"]
tags: ["php","facebook","login"]
slug: "php-facebook-login-yeni-api"
---


***Facebook***'un yeni API sürümü ile PHP kullanarak Login sistemi geliştirelim,

İlk olarak Composer ile Facebook bağlantılarımızı yapmak için gerekli sınıfları indirelim

    composer require facebook/graph-sdk

Şimdi Facebook üzerine dönelim [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/) adresine girip Uygulama oluşturuyoruz,

Local üzerinde çalışıyorsak, local adresimiz de yazmalıyız,

Facebook üzerinde app oluşturma için hızlı bir video çektim,
<iframe width="560" height="315" src="https://www.youtube.com/embed/8jc8uHMKhbA" frameborder="0" allowfullscreen></iframe>

Şimdi devam edelim

    require_once __DIR__ . '/vendor/autoload.php'; // bu dizini kendinize göre düzenleyin

    $fb = new \Facebook\Facebook([
    'app_id' => 'VİDEODAKİ APP ID',
    'app_secret' => 'VİDEODAKİ SECRET',
    'default_graph_version' => 'v2.10',
    ]);
    $helper = $fb->getRedirectLoginHelper();

    try {
    $accessToken = $helper->getAccessToken();
    } catch(Facebook\Exceptions\FacebookResponseException $e) {
    
    echo 'Graph hata ile döndü ' . $e->getMessage();
    exit;
    } catch(Facebook\Exceptions\FacebookSDKException $e) {
  
    echo 'Facebook SDK hata ile döndü' . $e->getMessage();
    exit;
    }

    if (! isset($accessToken)) {
    if ($helper->getError()) {
        header('HTTP/1.0 401 Unauthorized');
        echo "Error: " . $helper->getError() . "\n";
        echo "Error Code: " . $helper->getErrorCode() . "\n";
        echo "Error Reason: " . $helper->getErrorReason() . "\n";
        echo "Error Description: " . $helper->getErrorDescription() . "\n";
    } else {
        header('HTTP/1.0 400 Bad Request');
        echo 'Bad request';
    }
    exit;
    }

    
    echo '<h3>Access Token</h3>';
    var_dump($accessToken->getValue());

    
    $oAuth2Client = $fb->getOAuth2Client();

    
    $tokenMetadata = $oAuth2Client->debugToken($accessToken);
    echo '<h3>Metadata</h3>';
    var_dump($tokenMetadata);

    
    $tokenMetadata->validateAppId('{app-id}'); // app id ile değiştirin
    $tokenMetadata->validateExpiration();

    if (! $accessToken->isLongLived()) {
    try {
        $accessToken = $oAuth2Client->getLongLivedAccessToken($accessToken);
    } catch (Facebook\Exceptions\FacebookSDKException $e) {
        echo "<p>Uzun süren access token alınamadı: " . $helper->getMessage() . "</p>\n\n";
        exit;
    }

    echo '<h3>Uzun süreli token</h3>';
    var_dump($accessToken->getValue());
    }

    $_SESSION['fb_access_token'] = (string) $accessToken;
    $response = $fb->get('/me?fields=id,name', $accessToken);

    $user = $response->getGraphUser();

    echo 'Name: ' . $user['name'];

Şimdi ilk dikkat edeceğimiz şey, permissions kısmı. Buraya ekleyecekleriniz ile ilgili detayları [https://developers.facebook.com/docs/facebook-login/permissions/](https://developers.facebook.com/docs/facebook-login/permissions/) adresinden alabilirsiniz. 
Ek olarak uzun süreli token'ı 60 güne kadar kullanabilirsiniz, kısaca kullanıcı sisteminize facebook ile girdikten sonra buradaki long-lived token'i veritabanına kayıt edip, buradaki token ile adamın hesabından daha önce aldığınız izinler sınırında istediğinizi yaptırabilirsiniz.

