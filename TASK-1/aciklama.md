İsim - Soy isim ALİ İSTANBULLU
Öğrenci No:250542019

ATM Para Çekme Sistemi – Akış ve Mantık Açıklaması

ATM para çekme sistemi, kullanıcının güvenli bir şekilde hesabından para çekmesini sağlayan adım adım bir süreçtir. Bu sistem, hem kullanıcı hatalarını hem de bankacılık kurallarını dikkate alarak çalışır. Aşağıda her aşama detaylı şekilde açıklanmıştır:

1. Kart Takılır ve PIN Sorulur

Kullanıcı ATM’ye kartını takar ve sistem PIN (şifre) girmesini ister. Bu, işlemin güvenliğinin sağlanması için ilk adımdır.

2. PIN Doğrulama

Kullanıcı PIN’i girer.

Eğer PIN doğruysa işlem devam eder.

Yanlış girilirse hata sayısı 1 artar.

Üç kez hatalı giriş yapılırsa kart blokelenir ve işlem sonlandırılır. Bu adım, yetkisiz erişimi önler.

3. Bakiye Sorgulama

PIN doğruysa sistem kullanıcının hesabındaki bakiyeyi kontrol eder ve işlem için hazırlar.

4. Tutar Girişi

Kullanıcı çekmek istediği tutarı girer.

5. Yetersiz Bakiye Kontrolü

Eğer çekilmek istenen tutar, hesabındaki bakiyeyi aşarsa, sistem kullanıcıya “Yetersiz bakiye!” uyarısı verir.

Kullanıcıdan tekrar tutar girmesi istenir.

6. 20 TL’nin Katı Kontrolü

ATM yalnızca 20 TL’nin katları şeklinde para verebilir.

Girilen tutar 20’nin katı değilse, kullanıcıya “Tutar 20 TL’nin katı olmalı!” mesajı gösterilir ve tekrar tutar girmesi istenir.

7. Günlük Limit Kontrolü

Kullanıcının günlük para çekme limiti aşılmışsa, sistem “Günlük limit aşıldı!” mesajı verir.

Kullanıcı yeni bir tutar girebilir.

8. Para Verme ve Fiş Çıkarma

Tüm kontroller geçildiyse:

ATM hesabından tutarı düşer.

Para makineden verilir.

Fiş çıkarılır.
Bu adım işlemin başarılı bir şekilde tamamlandığını gösterir.

9. Başka İşlem Yapmak İster Misiniz?

İşlem tamamlandıktan sonra sistem kullanıcıya “Başka işlem yapmak ister misiniz?” sorusunu sorar.

Evet cevabı verilirse sistem tekrar menüye dönerek yeni işlemler yapılabilir.

Hayır cevabı verilirse kart iade edilir ve işlem güvenli bir şekilde sonlandırılır.

Sistem Mantığının Özeti

Güvenlik: PIN kontrolü ve 3 hatalı giriş sonrası kart bloke edilmesi.

Finansal Kontroller: Yetersiz bakiye, günlük limit ve 20 TL’nin katı kontrolü.

Kullanıcı Deneyimi: Hatalı durumlarda kullanıcı uyarılır ve tekrar giriş yapması sağlanır.

Başarılı İşlem: Tüm kontroller geçildiğinde para verilir ve fiş çıkarılır.

Tekrar İşlem: Kullanıcı isterse yeni işlem yapabilir, istemezse kart iade edilir ve işlem tamamlanır.
