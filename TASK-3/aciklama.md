AD-SOYAD = ALİ İSTANBULLU 
ÖĞRENCİ NO = 250542019

Bu sistem, temel bir hastane bilgi sisteminde hasta randevu alma ve tahlil sonucu görüntüleme süreçlerini yöneten bir akış şemasını ve mantığını temsil etmektedir.

Aşamalar:
Hasta Kimlik Doğrulama (Başlangıç ve Döngü):

Sistem başlar ve kullanıcıdan TC Kimlik Numarası istenir.

Girilen TC No'nun geçerliliği kontrol edilir. Geçersiz ise uyarı verilir ve tekrar TC No girmesi istenir (dış döngü).

İşlem Seçimi (Koşul):

Başarılı kimlik doğrulamadan sonra, kullanıcıya 1-Randevu Al veya 2-Tahlil Sonucu Gör seçenekleri sunulur.

Randevu Modülü (Döngü):

Kullanıcı '1'i seçerse, randevu akışı başlar.

Poliklinik Seçimi yapılır.

Seçilen polikliniğe ait Doktor Listesi görüntülenir.

Seçilen doktorun Uygun Saatleri getirilir.

Koşul: Uygun saat yoksa kullanıcı farklı bir doktor/poliklinik seçimine yönlendirilir (iç döngü).

Uygun saat seçimi sonrası Randevu Onayı istenir.

Onay verilirse randevu kaydedilir ve SMS Gönderimi yapılır. Ardından randevu döngüsünden çıkılır.

Tahlil Modülü (Koşullar):

Kullanıcı '2'yi seçerse, tahlil akışı başlar.

Koşul 1: Tahlil Var mı? Hastanın geçmişinde herhangi bir tahlil olup olmadığı kontrol edilir. Yoksa bilgi mesajı verilir ve akış biter.

Koşul 2: Sonuç Hazır mı? Tahlil varsa, sonuçların sistemde hazır olup olmadığı kontrol edilir.

Hazır İse: Sonuç Görüntüleme yapılır ve PDF İndirme Seçeneği sunulur.

Hazır Değil İse: Sonuçların henüz hazır olmadığına dair Bekleme Mesajı gösterilir.

Başka İşlem Sorgusu (Döngü):

Randevu veya Tahlil modülü tamamlandıktan sonra, kullanıcıya "Başka bir işlem yapmak ister misiniz?" sorusu sorulur.

'E' (Evet) yanıtı gelirse akış, TC Kimlik Doğrulama adımından itibaren tekrar başlar (ana döngü).

'H' (Hayır) yanıtı gelirse sistem kapanır.
