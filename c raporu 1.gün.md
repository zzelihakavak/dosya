## `	`**C RAPORU (1.GÜN)**
En aşağı seviyeli saf dil makine dilidir. Bu dil yalnızca 1 ve 0 lardan oluşur. C diğer dillere göre makine diline daha yakındır. 

*İşletim Sistemi(operating system):*   Kaynak yöneticisi gibi çalışan, makinanın donanımı yöneten temel sistem yazılımıdır. Temel pek çok hizmeti sağlar.  Kullanıcı ile makine donanımı arasında köprü kurar. 

*IDE Kavramı:* IDE derleyici değildir. Derle denildiği zaman gerçek derleyiciyi çağırır. 

*Sayı Sistemleri:* Makine ikilik sayı sistemini kullanır çünkü elektriksel olarak ifade edilmesi daha kolaydır. Bu alana dijital elektronik deriz. 

Bilgisayar yalnızca bellekteki bitleri tutar. Bit en düşük bellek birimidir. 8 bit=byte

Bilgisayar bilimlerinde kilo 1024 katı anlamına gelir. 

*Yazıların ikilik sistemde ifade edilmesi:* Her karakter 1 byte ile kodlanabilir. Yazılar ikilik sistemde kodlanmış olur. Hangi karakterin hangi sayıyla ifade edileceğini belirlemek için ASCII (American Standard Code Information Interchange) tablosu denilen bir tablo yaygın bir biçimde kullanılmaktadır.

*Bilgisayarın basit mimarisi:*Üç önemli birim vardır. CPU,RAM ve DİSK. CPU'lar entegre devre biçiminde üretilmektedir ve onlara mikroişlemci de denilmektedir. CPU ile elektriksel olarak bağlantılı olan ve CPU2nun çalışması sırasında sürekli kullanılan belleklere Ana Bellek (Main Memory) ya da Birincil Bellek (Primary Memory) denilmektedir. Bunlar RAM teknolojisiyle üretildiklerinden bunlara RAM de denir. Bilgisayarın güç kaynağı kesilince ana bellekteki bilgiler kaybolduğu için bellekteki bilgileri tutan birime ihtiyaç duyulmuştur. Bu birimlere a İkincil Bellekler (Secondary Storage Devices) denir. 

*Bir C programı oluşturmak:* Kaynak dosya oluşturulur,  dosya derleyici tarafından derlenir, amaç dosyalar bağlayıcı program tarafından birleştirilerek çalıştırılabilir dosya oluşturulur. 

*Atom(token) kavramı:* Programlama dilindeki anlamlı en küçük birimdir. 6 gruba ayrılır. Anahtar sözcükler, değişkenler, sabitler, operatörler, stringler, ayıraçlar
\*


*Bazı matematiksel C fonksiyonları:*

<math.h> include edilir.

Sqrt aldığı değerin karekökünü geri gönderir.

Pow fonksiyonu üs almak için kullanılır. birinci parametresiyle belirtilen değerin ikinci parametresiyle belirtilen kuvvetini alır ve onu geri dönüş değeri olarak verir.

log fonksiyonu e tabanına göre log10 fonksiyonu 10 tabanına göre logaritma alır.

sin, cos, asin, acos, tan, atan fonksiyonları trigonometrik işlemleri yapar. Bu fonksiyonlardaki açılar radyan cinsinden girilmelidir.

exp fonksiyonu e üzeri işlemi yapmaktadır.

*Sabitler:*

1) Sayı nokta içermiyorsa ve sayının sonunda hiçbir ek yoksa sabit int, long ve unsigned long türlerinin hangisinin sınırları içerisinde ilk kez kalıyorsa o türdendir.
1) ` `Sayı nokta içermiyorsa ve sayının sonuna küçük harf ya da büyük harf L getirilmişse sabit long ve unsigned long türlerinin hangisinin sınırları içerisinde ilk kez giriyorsa o türdendir.
1) Sayı nokta içermiyorsa ve sayının sonunda küçük harf ya da büyük harf U varsa sabit unsigned int ve unsigned long türlerinin hangisinin sınırları içerisinde ilk kez kalıyorsa o türdendir.
1) Sayı nokta içermiyorsa ve sayının sonunda küçük harf ya da büyük harf UL ya da LU varsa (UL, Ul, uL, LU, Lu, ul, lu) sabit unsigned long türündendir
1) Sayı nokta içeriyorsa ve sayının sonında hiçbir ek yoksa sabit double türdendir
1) Sayı nokta içeriyorsa ve sayının sonunda küçük harf ya da büyük harf F varsa sabit float türdendir
1) Sayı nokta içeriyorsa ve sonunda küçük harf ya da büyük harf L varsa sabit long double türdendir.


