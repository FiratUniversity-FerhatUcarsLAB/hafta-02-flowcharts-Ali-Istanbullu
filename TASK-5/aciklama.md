İSİM-SOYİSİM = ALİ İSTANBULLU
ÖĞRENCİ NO = 250542019
Başlangıç

Akış “BASLA” düğümüyle başlar.

İlk kontrol: Sistem aktif mi?

Eğer hayır → sistem çalıştırılamaz, uyarı verilir ve işlem bitirilir.

Eğer evet → bir sonraki adım gece mi gündüz mü sorusudur.

 Gece / Gündüz Kontrolü

Gece ise: Gece görüş kamerası açılır.

Gündüz ise: Normal kamera çalışır.

Bu adım, sistemin sensör ve kameralarını uygun ışık koşullarına göre hazırlar.

 Sonsuz Döngü: Sensör ve Alarm Kontrolü

Sistem aktif olduktan sonra, sürekli sensör okuma döngüsü başlar. Döngü, aşağıdaki adımları tekrar eder:

3a. Ev Sahibi Kontrolü

Ev sahibi evde mi? sorulur:

Ev sahibi evdeyse:

Sensörler yine çalıştırılır.

Hareket sensörü + ısı sensörü kontrol edilir.

Eğer hareket var ve ısı > 30°C (insan) → Seviye 1 alarm çalışır.

Kamera açılır ve uyarı gönderilir.

Bu şekilde, ev sahibi var olsa bile potansiyel tehlike tespit edilebilir.

Ev sahibi yoksa:

Sensörler çalıştırılır ve insan/hayvan ayrımı yapılır:

Hareket yok → döngü bekler ve tekrar başlar.

Hareket var ama ısı ≤30°C → hayvan veya nesne, alarm çalışmaz.

Hareket var ve ısı >30°C → insan var → yüz tanıma çalıştırılır.

3b. Yüz Tanıma ve Alarm Seviyeleri

Tanıdık kişi: Seviye 1 alarm → kamera + uyarı.

Tanınmadık kişi: Seviye 2 alarm → kamera + uyarı + kapılar ve pencereler kilitlenir.

Maskeli kişi (gizli):

Eve girmedi → Seviye 3 alarm → kamera + uyarı + kapılar ve pencereler kilitli.

Eve girdiyse → Seviye 3 + sis sistemi → sis sistemi çalıştırılır + kapılar/pencereler zaten kilitli.

 Bildirim ve Döngü

Her alarm seviyesinde, sistem SMS, uygulama ve email ile bildirim gönderir.

Döngü sonunda “Bekle ve tekrar kontrol et” adımıyla sonsuz döngü sağlanır.

Böylece sistem sürekli aktif kalır ve yeni hareketleri, yüzleri veya tehlikeleri tespit eder.

 Özet Mantık

Başta sistemin aktifliği ve ışık durumu kontrol edilir.

Ev sahibi durumu, hareket ve ısı sensörleri ile birleştirilerek Seviye 1 alarm yönetilir.

Ev sahibi yoksa yüz tanıma ile 1/2/3 alarm seviyesi belirlenir.

Seviye 3’te eve girilirse sis sistemi devreye girer.

Tüm alarm olayları bildirim gönderir ve sistem sürekli kontrol döngüsünde kalır.
