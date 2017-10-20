---
title: "Php ile CPP kodları çalıştırmak"
date: 2017-10-13T14:52:13+03:00
konular : ["php","cpp"]
tags: ["php","cpp"]
slug: "php-kodu-icerisinde-cpp-kodu-calistirma"
---


***PHP*** geliştirirken bazı durumlarda başka dillerden desteğe ihtiyacınız olabilir. PHP içerisinde benim en çok ihtiyacım olan dil genellikle ***cpp*** oluyor. Bu yazı da PHP kodu içerisinde örnek CPP kodları çalıştırabileceğimiz bir kaç yöntem üzerine konuşalım istedim.

İlk kurgumuz şu şekilde, C++ ile yazılmış veya yazacağımız bir yapımız var, bunu PHP içerisinde kullanmak istiyoruz. Ne yapmalıyız? ***Cevap*** Wrapper kodlamak. PHP'nin yazdığımı kodu anlayabilmesi için bir eklenti geliştirmek. 

İkinci kurgumuz, o kadar büyük abartılı değil basit olarak ne yapılabilir. Bu soru üniversitede ya da lise de ödev sorusu gibi gözüküyor. Bunu hemen cevaplayalım, php-cpp diye bir eklentimiz var. PHP için eklenti geliştirmeyi çok kolay hale getiriyor.

Bu yazıda ikinci kurgudan ilerliyoruz. Çünkü işlerimiz acil ve pratik çözüme ihtiyacımız var.

İlk olarak söyliyeyim, bu sistemin geliştiricisi sadece Linux dağıtımları kullandığı için Windows üzerinde çalışıp çalışmamasını umursamamış.

Hadi başlayalım,


    $ git clone https://github.com/CopernicaMarketingSoftware/PHP-CPP.git

Linux bir makinedeysek, yapmamız gereken tek şey dizine girip ***make*** komutunu çalıştırıp eklentiyi inşaa etmek.

Eğer MacOS üzerindeyseniz ***makefile*** üzerinde bir değişiklik yapmanız gerekiyor. makefile dosyasını açın ve ***LINKER_FLAGS***  gelip ***-undefined dynamic_lookup*** tanımlamasını ekleyin.

    $ sudo make install

Dediğimizde PHP-CPP eklentisi inşaa edilmiş olacak.

Linux üzerinden devam ediyoruz.

***Makefile*** dosyamızı düzenleyelim

    NAME                =   cilgineklentim
    UBUNTU_MAJOR  := $(shell /usr/bin/lsb_release -r -s | cut -f1 -d.)
    OVER_SIXTEEN  := $(shell echo "${UBUNTU_MAJOR} >= 16" | bc)
    OVER_FOURTEEN := $(shell echo "${UBUNTU_MAJOR} >= 14" | bc)

    ifeq (${OVER_SIXTEEN}, 1)
        INI_DIR     =   /etc/php/7.0/mods-available/
    else ifeq (${OVER_FOURTEEN}, 1)
        INI_DIR     =   /etc/php5/mods-available/
    else
        INI_DIR     =   /etc/php5/conf.d/
    endif
    EXTENSION_DIR       =   $(shell php-config --extension-dir)
    EXTENSION           =   ${NAME}.so
    INI                 =   ${NAME}.ini
    COMPILER            =   g++
    LINKER              =   g++
    COMPILER_FLAGS      =   -Wall -c -O2 -std=c++11 -fpic -o
    LINKER_FLAGS        =   -shared
    LINKER_DEPENDENCIES =   -lphpcpp
    RM                  =   rm -f
    CP                  =   cp -f
    MKDIR               =   mkdir -p
    SOURCES             =   $(wildcard *.cpp)
    OBJECTS             =   $(SOURCES:%.cpp=%.o)
    all:                    ${OBJECTS} ${EXTENSION}
    ${EXTENSION}:           ${OBJECTS}
                            ${LINKER} ${LINKER_FLAGS} -o $@ ${OBJECTS} ${LINKER_DEPENDENCIES}
    ${OBJECTS}:
                            ${COMPILER} ${COMPILER_FLAGS} $@ ${@:%.o=%.cpp}
    install:        
                            ${CP} ${EXTENSION} ${EXTENSION_DIR}
                            ${CP} ${INI} ${INI_DIR}
    clean:
                            ${RM} ${EXTENSION} ${OBJECTS}



***cilgineklemtim.ini*** dosyamız da eklentimizi tanımlıyoruz
    extension=cilgineklentim.so

***Main.cpp**
    #include <phpcpp.h>
    #include <iostream>

    void MerhabaCinim (Php::Parameters &params)
    {
        std::string name=params[0];
        std::cout<<"Selams "<<name<<"!"<<std::endl;

    }
    extern "C" {
        PHPCPP_EXPORT void *get_module() 
        {
            //statik olmasının nednei Php:extension tüm işlem süresince ram'de bulunmalı.
            static Php::Extension extension("cilgineklentim", "1.0");
            extension.add("MerhabaCinim", MerhabaCinim);
                   return extension;
        }
    }


Örnek bir eklenti ve bir fonksiyon hazırladık, şimdi derleyelim
    make && sudo make install

Ardından dosyaları php'mizin bulunduğu dizine ve eklenti dizinine ekliyoruz.
    cp -f skeleton.so /usr/lib/php5/20121212
    cp -f skeleton.ini /etc/php5/cli/conf.d

Eğer eklenti dizinini bilmiyorsanız hemen,

    apt-get install php-config
    php-config --extension-dir

ile öğrenebilirsiniz.Bi dk durun sakin olun gerek yok 
    php -i | grep extension_dir

ile de görebiliyorsunuz :)

Ardından php'mizin bu eklentiyi yükleyip yüklemediğini görelim

    php -i | grep cilgineklentim

Bu komut sonrasında ekranda hem eklentimizin ini dosyası yolu hem de adı yazmalı

Artık php içerisinde eklentimizi kullanabiliriz

    <?php

    echo MerhabaCinim('naptin');

İşin en temeli bu, abartmak isteyenler için,[bu adres](http://www.php-cpp.com/documentation) birebir.
