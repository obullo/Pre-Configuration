
Acceptance Tests
======
İlk olarak tests ayarlarımızı yapılandıralım.

![enter image description here](https://lh4.googleusercontent.com/-alf64_6IB5Q/VNTR9SluSYI/AAAAAAAAAL8/powc2uebO5A/s0/68747470733a2f2f6c68362e676f6f676c6575736572636f6e74656e742e636f6d2f2d71492d723853416169636f2f564c354249347163717a492f4141414141414141414b452f2d61436c334b39644f57732f73302f53637265656e73686f742b66726f6d2b323031352d30312d32302b31303a34343a30362e706e67.png "68747470733a2f2f6c68362e676f6f676c6575736572636f6e74656e742e636f6d2f2d71492d723853416169636f2f564c354249347163717a492f4141414141414141414b452f2d61436c334b39644f57732f73302f53637265656e73686f742b66726f6d2b323031352d30312d32302b31303a34343a30362e706e67.png")

Projemizin ana (root) dizinindeki tests klasörü içinde acceptance.suit.yml dosyamızı yukarıdaki şekilde yapılandırdık.

Ardından yeni bir test sınıfı oluşturalım:
```sh
$ codecept generate:cept acceptance First
```
Komutu çalıştırdıktan sonra **tests/acceptance** klasörü içinde **FirstCept.php** adında yeni bir dosyanın oluştuğunu göreceksiniz.

Şimdi yeni oluşturduğunuz test dosyamıza aşağıdaki senaryoyu ekleyelim.
```php
<?php
	$I = new AcceptanceTester($scenario);
	$I->wantTo('sign in');
	$I->amOnPage('/login');
	$I->fillField('username', 'davert');
	$I->fillField('password', 'qwerty');
	$I->click('LOGIN');
	$I->see('Welcome, Davert!');
?>
```

Yukarıdaki senaryoyu kısaca incelersek;

- **AcceptanceTester** classını çalıştırdık.
- Senaryo için bir amaç yada başlık  belirledik. **(wantTo)**
- Sonrasında **login** sayfasına gittik.
- **login** sayfasında **id/name** username olan inputa **'davert'** değerini girdik.
- **login** sayfasında **id/name** password olan inputa **'qwerty'** değerini girdik.
- Value **LOGIN** olan butona tıkladık.
- Formumuzun başarı durumunda vereceği mesajı **Welcome, Davert!** olarak kabul edip bunu sayfada aradık.

Şimdi testimizi çalıştıralım:
```sh
$ codecept run acceptance --steps
```

Yukarıdaki senaryo başarılı olursa şayet testlerin geçildiğine dair bir mesaj görülecektir. AKsi taktirde gene başarız oldupuna dair sonuçlar düşecektir.


Daha detaylı senaryolar için linki ziyaret edin: http://codeception.com/docs/04-AcceptanceTests

##Selenium
İlk testi **PhpBrowser** modülünü kullanarak yaptık. Burada **javascript** kullanamayacağımızı hatırlatalım. Şayet javascript testlerinide kapsayan bir testing yapılacaksa burada **Selenium** kullanılması gerekmektedir.

**Kurulum:**<br />
1. Download [Selenium Server](http://docs.seleniumhq.org/download/)<br />
2. ``` $ java -jar selenium-server-standalone-2.xx.xxx.jar```


**Ayarlar:**

![enter image description here](https://lh6.googleusercontent.com/-_Xx8Hg2vk6s/VNh3mgiHkGI/AAAAAAAAAMQ/opJ15Yj2QpM/s0/Screenshot+from+2015-02-09+11:00:50.png "Screenshot from 2015-02-09 11:00:50.png")

Selenium için ilgili ortamı hazırladıktan sonra test senaryolarını aynı PhpBrowser da olduğu gibi yazabiliyoruz. Birbirlerine karşı ufak farklılıklar dışında tamamen aynıdır.
