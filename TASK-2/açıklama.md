İSİM-SOYİSİM : ALİ İSTANBULLU
OKUL NO:250542019

ONLINE ALIŞVERİŞ SİSTEMİ AKIŞ AÇIKLAMASI 

A2: Kullanıcı Giriş Kontrolü (Koşul)
Sisteme erişim için kullanıcının kimlik bilgileri (Kullanıcı Adı/Şifre) kontrol edilir. Başarısız giriş denemelerinde, kullanıcı bir döngü aracılığıyla tekrar giriş yapmaya zorlanır.

B1-B6: Ürün Gezinme/Sepete Ekleme (Döngü)
Kullanıcının ürün kategorileri ve listeleri arasında gezinebildiği, ürün seçip miktarlarını belirleyerek sepete ekleme yaptığı ana alışveriş döngüsüdür.

B3: Stok Kontrolü (Koşul)
Sepete eklenmek istenen ürün miktarı mevcut stok ile karşılaştırılır. Yetersiz stok (Hayır) durumunda, sistem kullanıcıya uyarı verir (B5) ve yeni bir ürün seçimi yapması için B1 (Ürün Gezinme) aşamasına geri yönlendirir.

C1-C2: Sepet Görüntüleme/Düzenleme (Döngü)
Kullanıcı, sepetindeki ürünleri görüntüler, miktarını değiştirir veya ürün siler. Kullanıcı "Devam Et" diyene kadar bu düzenleme döngüsü devam eder.

C3: Minimum 50 TL Kontrolü (Koşul)
Siparişi tamamlama sürecine geçmeden önce sepetin toplam tutarının minimum 50 TL şartını sağlayıp sağlamadığı kontrol edilir. Şart sağlanamazsa (Hayır), kullanıcı zorunlu olarak tekrar B1 (Ürün Gezinme) aşamasına yönlendirilir.

D1: İndirim Kodu Uygulanacak mı? (Koşul)
Kullanıcının bir indirim kodu kullanmak isteyip istemediği ve girilen kodun geçerli olup olmadığı kontrol edilir. Geçerli kod varsa indirim uygulanır (D2).

D4: Kargo Ücreti Kontrolü (Koşul)
Sepet toplam tutarının 200 TL'yi aşıp aşmadığı kontrol edilir. Aşan sepetler için kargo ücreti 0 TL (D5) olarak belirlenir.

E1: Ödeme Yöntemi Seçimi (Koşul)
Kullanıcıdan geçerli bir ödeme yöntemi seçmesi istenir. Geçerli bir yöntem seçilene kadar kullanıcı bir döngü içinde seçim yapmaya zorlanır (E2).

E3: Sipariş Onayı (Koşul)
Tüm kontroller tamamlanıp nihai tutar belirlendikten sonra, kullanıcıdan siparişi onaylaması istenir. Onaylanırsa sipariş oluşturulur (E4), aksi takdirde sipariş iptal edilir (E5).
