**Register Programlama**

İşlemci çalışması sırasında farklı amaçlar için kullanılan değişkenlerdir. Normalde bellekteki verilere ulaşmak için belli bir zaman gerekir. Register tipi değişkenlerin tanımlanma ve kullanılma nedeni, programın daha etkin ve daha hızlı çalışır hale getirilme isteğidir. Çünkü doğal olarak, bilgisayarın CPU yazmacındaki bir veriye ulaşma zamanı bir bellek hücresindeki veriye ulaşma zamanına göre çok daha kısadır.

Ama registerler işlemci çekirdeğindedir ve fazladan zaman harcamadan istenen işleme göre kullanılır.

|<p><br> </p><p><--- 32 bit register ---></p>||||
| :-: | :-: | :-: | :-: |

|EAX|
| :-: |
|EBX|
|ECX|
|EDX|
|EBP|
|ESP|
|ESI|
|EDI|

|<br> |<--- 16 bit register --->|||
| :-: | :-: | :-: | :-: |

|AH|AL|
| :-: | :-: |
|BH|BL|
|CH|CL|
|DH|DL|

|||||
| :-: | :-: | :-: | :-: |

|BP|
| :-: |
|SP|
|SI|
|DI|

|||<br><--- 16 bit register --->||
| :-: | :-: | :-: | :-: |

|CS|
| :-: |
|DS|
|SS|
|ES|
|FS|
|GS|

||||<--- 32 bit register --->|
| :-: | :-: | :-: | :-: |

|EIP|
| :-: |
|EFLAGS|

|||||
| :-: | :-: | :-: | :-: |
Registerlerin sınıflandırılmış hallerinin tablosu da bu şekildedir;

|Data Registers|Pointer Registers|Index Registers|Segment Registers|
| :-: | :-: | :-: | :-: |
|EAX,EBX,ECX,EDX,AX,BX,CX,DX,AH,AL,BH,BL,CH,CL,DH,DL|EBP,ESP,BP,SP|ESI,EDI,SI,DI|CS,DS,SS,ES,FS,GS|


Boyutlarına göre sınflandırılmış hali;

|32bit registers (4 byte)|16bit registers (2 byte)|8bit registers (1 byte)|
| :-: | :-: | :-: |
|EAX,EBX,ECX,EDX,EBP,ESP,ESI,EDI,<br>EIP,EFLAGS|AX,BX,CX,DX,BP,SP,SI,DI,<br>CS,DS,SS,ES,FS,GS,IP,FLAGS|AH,AL,BH,BL,CH,CL,DH,DL|

Hangi register ne işe yarar?

AX : Akümülatör Registeri, Dörtişlem operasyonlarında kullanılmaktadır.

BX : Base Registeri, Bellek lokasyonlarında baz adres göstericisi olarak kullanılır, yani bir tür index registeri gibi kullanılabilir.

CX : Counter Registeri, Döngü işlemlerinde sayaç olarak kullanılır, yani döngü kaç defa daha dönecek bunun sayısını tutar.

DX : Data Registeri, Donanım ile yapılan giriş çıkış işlemlerinde kullanılır.

CS : Code Segment Registeri, Segmentler bellekte bir alt bölümü işaret ederler.En önemli segmenttir. İçeriğinde yazılan programın komutları yer alır. Hem programcı hemde kullanılan işletim sistemi kod segmentteki komutlar üzerine başka dataların yazılmayacağının garantisini almak zorundadır. Aksi taktirde program garip hatalar verir ve kitlenir.

DS : Data Segment Registeri, programı yazarken kullandığımız değişkenler,karakter dizileri ayrıca çalışma anında oluşturulan değişken tiplerinin tamamı bu segment altında tutulur.

SS : Stack Segment Registeri, Stack özel bir data segment tipidir. Alt programlardan, dll dosyaları içinde bulunan fonksiyonlardan, windows api fonksiyonlarından kodlar yürütülmeden önce gerekli değişkenler bu segmente sadece bu amaçla kullanılan bir assembly komutu ile alınırlar. Daha sonra çağırma işlemi yapılır. Önemli olan çalışma prensibini anlamaktır. Burada diğer data segmentlerden olduğu gibi istenilen adresinden veri çekilebilmektedir. Farkı ise stack'a yollanan son verinin çağırılma esnasında ilk olarak geri dönmesidir. Yani son giren-ilk çıkar mantığı. Stacka son yollanan veriyi SP isimli Stack Pointeri işaret eder.

ES : Extra Data Segment Registeri,Data segment ile aynı özelliklere sahiptir. Özel olarak bu segmenti kullanan birkaç komut bulunmaktadır.

FS,GS : Bu segment registerleri ihtiyaç olduğu zaman kullanılmaktadır. Aslında ek olarak kullanılan Data Segment Registerleridir.

BP : Base Pointer, Stack segmentin başlangıç noktasını gösterir. Yani genelde içeriği sıfırdır.

SP : Stack Pointer, Stack segment içine gönderilmiş olan son değerin (byte) adresini göstermektedir. Stack içine veriler yollandıkça değeri azalır çünkü veri segmetin sonundan başına doğru alınırlar. Veriler stackten çekildikçe değeri artar, böylece eski verileri gösterir, eski veriler silinmez ama SP değeri değiştiği için işlem hata vermeden yürümektedir.
\*BP ve SP aslında SI ve DI gibi segmentler içindeki verinin adresini gösterirler. Stack Segmentin özel bir çalışma şekli olduğu için bu Pointer registerleri özel olarak sadece Stack Segmentin sağlıklı çalışması için görev yapmaktadır.

SI : Source Index, Data segment veya istenirse başına küçük bir tanımlama eklenerek diğer data segmentlerdeki verileri de göstermek için kullanılan bir index (işaretçi) registerdir.

DI : Destination Index, SI ile tamamen aynı özelliklere sahiptir. Fakat SI ve DI bazı string komutları tarafından kaynak ve hedef işaretçisi olarak da kullanılmaktadır.

IP : Bir işaretçi registerdir. Code Segment içinde işlenecek bir sonraki komutun yerini işaret eder. 

FLAGS : 32 bitlik bir registerdir. Bu registerin içeriğindeki bitler çok önemlidir. Bazı bitler anlamsızdır, diğerleri ise daha önce işlenen komutların sonuçları ile ilgili bilgiler verir. Örneğin CMP komutu ile iki sayı karşılaştırılır ise sayıların eşit olma veya birinin diğerine göre büyük olması bu register içindeki bazı bitleri 1 (set) veya 0 (reset) durumuna getirecektir. Daha sonra kullanılacak bir dallanma komutu ile bu flaglar kontrol edilerek sonuca göre belirli adreslere dallanmalar yapılır. İçeriğini direkt olarak kullanamayız . Bazı komutlar işleyişleri sırasında bu registeri gizli olarak kullanmaktadırlar.

Register sınıfındaki değişkenlere bellek yerine yazmaçlarda yer ayrıldığı için bu değişkenlerin başına bellek adresi operatörü olan & sembolü konulamaz. Bir değişken, bir gösterge işlemleri içinde kullanılacaksa bu  durumda bu değişken register tipinde tanımlanmamalıdır.







ÖRNEK:

#import <Foundation/Foundation.h>

int main(int argc,char \*argv[])

{

`    `NSAutoreleasePool \*pool=[[NSAutoreleasePool alloc] init];



`    `int s=0;

`    `{

`        `register i;

`        `for (i=1; i<=100; i++)

`            `s+=i;

`    `}

`    `NSLog(@"\n1+2+..100=%i\n\n",s);

`    `[pool drain];

`    `return 0;

}

` `PROGRAMIN ÇIKTISI:

1+2+..100=5050

Yukarıdaki programda, içteki bloktan çıkılınca i’nin değeri aşağıdaki gibi yazdırılmak istenirse:

![metin, ekran görüntüsü, yazı tipi, çizgi içeren bir resim

Açıklama otomatik olarak oluşturuldu](Aspose.Words.2d175a76-6a48-4790-925d-d8dff736b0b6.001.png)

!!!!

Register seviyesinde kodlama yaparken, en önemli süreç, doğrudan donanım kaynaklarının kontrolünü ele almak ve bu kaynakları verimli bir şekilde yönetmektir. Bu süreçte, doğru registerleri seçmek, uygun bit manipülasyonu yapmak ve donanımın istenen davranışını elde etmek için gerekli ayarlamaları yapmak kritiktir. Ayrıca, kodun optimize edilmesi ve kaynakların verimli kullanılması da önemli bir adımdır. Bu süreç, genellikle dikkatli planlama, test ve doğrulama gerektirir, ancak donanım üzerinde tam kontrol sağlar ve performansı maksimize etmeye olanak tanır.


