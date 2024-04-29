![](Aspose.Words.cd0a56d5-571e-41b1-8a9b-430f1d5be5d2.001.png)                                  **SoC (State of Charge)**


![](Aspose.Words.cd0a56d5-571e-41b1-8a9b-430f1d5be5d2.002.png)\*Bir elektrik pilinin kapasitesine göre şarj seviyesidir. 

\*SoC birimleri yüzde puandır (%0 = boş; %100 = dolu). Aynı ölçümün alternatif bir biçimi, deşarj derinliğidir (DoD), SoC'nin tersidir (%100 = boş; %0 = dolu).
### ![metin, çizgi, yazı tipi, öykü gelişim çizgisi; kumpas; grafiğini çıkarma içeren bir resim

Açıklama otomatik olarak oluşturuldu](Aspose.Words.cd0a56d5-571e-41b1-8a9b-430f1d5be5d2.003.jpeg) 

**Lityum İyon Şarj Durumu (SoC) ölçümü**

1. Açık Devre Gerilim Yöntemi (OCV) kullanılarak SoC tahmini
1. Coulomb Sayımı yöntemini kullanarak SoC tahmini

**Lityum Polimer Pillerde Kullanılacak SoC (Şarj Durumu) Yazılımı**

LiPo piller, Li-ion pillere göre daha hassastır ve aşırı şarj veya aşırı deşarjdan daha kolay etkilenebilirler. Bu nedenle, LiPo piller için özel olarak tasarlanmış SoC yazılımı kullanmak daha mantıklıdır.

**Pil sağlığı izleme:** Pilin kapasitesinin zamanla nasıl değiştiğini ve ne zaman değiştirilmesi gerektiğini belirlemek için kullanılır.

**Pil Voltajı Takibi:** SoC yazılımı, pil hücrelerinin voltajını sürekli olarak izler. Bu bilgiler, pilin ne kadar şarjlı olduğunu ve şarj veya deşarj işleminin ne zaman durması gerektiğini belirlemek için kullanılır.

` `**Akım Takibi:** Yazılım, pil hücrelerinden geçen akımı da izler. Bu bilgi, şarj veya deşarj işleminin ne kadar hızlı gerçekleştiğini belirlemek için kullanılır. 

**Pil Sıcaklığı Takibi:** SoC yazılımı, pilin sıcaklığını da izler. Sıcaklık, pilin kimyasal reaksiyonlarının hızını önemli ölçüde etkileyebileceğinden bu önemlidir. Yazılım, pilin aşırı ısınmasını önlemek için şarj veya deşarj işlemini otomatik olarak ayarlayabilir.** 

**Kalan Şarj Hesaplama:** Yazılım, toplanan voltaj, akım ve sıcaklık verilerini kullanarak pilin kalan şarjını tahmin eder. Bu bilgi, kullanıcı arayüzünde gösterilebilir veya pilin ne kadar süre dayanacağını tahmin etmek için kullanılabilir.

**SoC Yazılımı Çeşitleri**

1. Basit SoC Yazılımı: Temel pil izleme ve koruma fonksiyonları
1. Gelişmiş SoC Yazılımı: Daha karmaşık pil izleme ve yönetim fonksiyonları

   **Örnek 1**

   **C Kodu (Arduino için)**

   LİPO-Pil voltajını, şarj akımını, sıcaklığını okumak için Arduino da pin tanımlarız (**const int** ile). Daha sonra seri haberleşmeyi başlatıp giriş pinlerini ayarlayıp okuma işlemlerine **void loop** ile başlıyoruz.Okunan değerleri Serial.print ve Serial.println ile yazdırıyoruz. 

#include <Arduino.h>

const int voltagePin=A0;

const int currentPin=A1;

const int temperaturePin=A2;

const float voltageDividerRatio = 2.0; //voltaj bölücü varsa

void setup(){

`  `Serial.begin(9600); //seri haberleşmeyi başlatıyoruz.

`  `pinMode(voltagePin,INPUT);

`  `pinMode(currentPin, INPUT); // voltaj akım pinlerini giriş pinleri olarak ayarladık.

`  `if (temperaturePin != -1) {

`    `pinMode(temperaturePin, INPUT);  //değişkeninin değeri -1'e eşit değilse, kod bloğu yürütülür. Bu, sıcaklık sensörünün var olduğunu ve pini giriş pini olarak ayarlamak gerektiğini gösterir.

`    `//değişkeninin değeri -1'e eşitse, kod bloğu atlanır. Bu, sıcaklık sensörünün olmadığı anlamına gelir ve bu nedenle pini ayarlamak gerekli değildir.

`  `}

}

void loop() {

`  `float voltage= analogRead(voltagePin)\*voltageDividerRatio \*5.0/1024.0;

`  `int current= analogRead(currentPin);

`  `float temperature = -1.0;

`  `if (temperaturePin != -1) {

`    `temperature = analogRead(temperaturePin) \* 5.0 / 1024.0;

`  `}

`  `float calculateRemainingCharge(float voltage, float capacity) {

`  `// Kalan şarjı hesapla

`  `float remainingCharge = voltage \* capacity;

`  `// Kontrol edin ve gerekirse kalan şarjı 0'a ayarlayın

`  `if (remainingCharge < 0.0) {

`    `remainingCharge = 0.0;

`  `}

`  `// Kalan şarjı yüzdesine dönüştür

`  `float remainingChargePercentage = (remainingCharge / capacity) \* 100.0;

`  `// Dönüş

`  `return remainingChargePercentage;

}

//şimdi okunan değerleri seri monitöre yazdıralım.

Serial.print("Voltaj:");

Serial.print(voltage);

Serial.println(" V");

Serial.print("Akım:");

Serial.print(current);  //serial.println satıra otomatik olarak \n ekler.

Serial.println("mA");

` `if (temperaturePin != -1) { //if yapısı kullanmamızın nedeni sıcaklık sensörünün varlığını kontrol etmektir.

`    `Serial.print("Sıcaklık: ");

`    `Serial.print(temperature);

`    `Serial.println(" °C");

`  `}

`  `Serial.print("Kalan Şarj: ");

`  `Serial.println("%");

`  `Serial.println("----------------------");

`  `delay(1000); // 1 saniye bekle

}

}

**Örnek 2**

**C Kodu (STM32 için)**

#include <stm32f4xx.h> // Mikrodenetleyici kütüphaneleri

#include <adc.h> // ADC kütüphaneleri

#include <usart.h> // USART kütüphaneleri

// Kullanıcı tanımlı sabitler

#define ADC\_CHANNEL\_CURRENT ADC\_CHANNEL\_1 // Akım sensörü için ADC kanalı

#define ADC\_CHANNEL\_TEMPERATURE ADC\_CHANNEL\_2 // Sıcaklık sensörü için ADC kanalı

#define ADC\_CHANNEL\_VOLTAGE ADC\_CHANNEL\_3 // Voltaj sensörü için ADC kanalı

// Kullanıcı tanımlı fonksiyonlar

float readCurrent(); // Akım değerini oku

float readTemperature(); // Sıcaklık değerini oku

float readVoltage(); // Voltaj değerini oku

float calculateRemainingCharge(float voltage, float capacity); // Kalan şarjı hesapla

int main() {

`  `// Başlatma

`  `initADC(); // ADC'yi başlat

`  `initUSART(); // USART'yi başlat

`  `// Pil kapasitesini ayarla(mAh cinsinden)

`  `float capacity = 2000.0;

`  `// Sonsuz döngü

`  `while (1) {

`    `// Akım, sıcaklık ve voltaj değerlerini oku

`    `float current = readCurrent();

`    `float temperature = readTemperature();

`    `float voltage = readVoltage();

`    `// Kalan şarjı hesapla

`    `float remainingCharge = calculateRemainingCharge(voltage, capacity);

`    `// Seri monitöre değerleri yazdır

`    `Serial.print("Akım: ");

`    `Serial.print(current);

`    `Serial.println(" A");

`    `Serial.print("Sıcaklık: ");

`    `Serial.print(temperature);

`    `Serial.println(" °C");

`    `Serial.print("Voltaj: ");

`    `Serial.print(voltage);

`    `Serial.println(" V");

`    `Serial.print("Kalan Şarj: ");

`    `Serial.print(remainingCharge);

`    `Serial.println(" %");

`    `// Gecikme

`    `delay(1000); // 1 saniye bekle

`  `}

}

// Akım değerini oku

float readCurrent() {

`  `// ADC'yi oku ve akım sensörünün değerini dönüştür

`  `float adcValue = readADC(ADC\_CHANNEL\_CURRENT);

`  `float current = adcValue \* (maximumCurrent / 4096.0); // Ölçeğe göre dönüştürdük

`  `return current;

}

// Sıcaklık değerini oku

float readTemperature() {

`  `// ADC'yi oku ve sıcaklık sensörünün değerini dönüştür

`  `float adcValue = readADC(ADC\_CHANNEL\_TEMPERATURE);

`  `float temperature = (adcValue \* referenceVoltage) / (temperatureSensorSlope \* Vcc);

`  `return temperature;

}

// Voltaj değerini oku

float readVoltage() {

`  `// ADC'yi oku ve voltaj sensörünün değerini dönüştür

`  `float adcValue = readADC(ADC\_CHANNEL\_VOLTAGE);

`  `float voltage = (adcValue \* referenceVoltage) / (voltageSensorDivider \* Vcc);

`  `return voltage;

}

// Kalan şarjı hesapla

float calculateRemainingCharge(float voltage, float capacity) {



`  `float remainingCharge = voltage \* capacity;

`  `// Kontrol et ve gerekirse kalan şarjı 0'a ayarla

`  `if (remainingCharge < 0.0) {

`    `remainingCharge = 0.0;

`  `}

`  `// Kalan şarjı yüzdesine dönüştür

`  `float remainingChargePercentage = (remainingCharge / capacity) \* 100.0;

`  `// Dönüş

`  `return remainingChargePercentage;

}




**KAYNAKÇA**

[**https://www.lithium-battery-factory.com/tr/lithium-battery-state-of-charge/**](https://www.lithium-battery-factory.com/tr/lithium-battery-state-of-charge/)

[**https://www.youtube.com/watch?v=w4kxKJYPlTY**](https://www.youtube.com/watch?v=w4kxKJYPlTY)

[**https://www.youtube.com/watch?v=dRKCgDl_yrg**](https://www.youtube.com/watch?v=dRKCgDl_yrg)

[**https://www.youtube.com/watch?v=7DTzShuFN6M**](https://www.youtube.com/watch?v=7DTzShuFN6M)



