AD-SOYAD = ALİ İSTANBULLU
ÖĞRENCİ NO = 250542019

Bu sistem, kullanıcının ders ekleme işlemini bir döngü içinde tamamlamasına ve bu işlemden sonra kaydı sonlandırma kararı vermesine olanak tanır. Akış şu şekilde işler:

Giriş: Süreç, öğrencinin numarası ve şifresiyle sisteme giriş yapmasıyla başlar. Giriş bilgileri yanlışsa, kullanıcı doğru bilgileri girene kadar bu adım tekrarlanır.

Bilgilendirme: Başarılı girişin ardından, öğrencinin seçebileceği tüm derslerin listesi ekranda gösterilir.

Ders Ekleme Döngüsü (Başlangıç): Kullanıcıya doğrudan eklemek istediği dersin bilgisini girmesi için bir ekran sunulur. Bu adım, ders ekleme döngüsünün başlangıç noktasıdır.

Dört Aşamalı Kontrol: Girilen ders için sistem sırasıyla şu kontrolleri yapar:

Kontenjan Kontrolü: Derste boş yer var mı?

Ön Koşul Kontrolü: Öğrenci, bu dersin ön koşulunu sağlıyor mu?

Zaman Çakışması Kontrolü: Ders, öğrencinin daha önce eklediği başka bir dersle çakışıyor mu?

Kredi Limiti Kontrolü: Bu dersin eklenmesi, toplam kredi limitini (35) aşıyor mu?

Hata Yönetimi: Yukarıdaki kontrollerden herhangi biri başarısız olursa, ekranda ilgili hata mesajı (örn: "HATA: Kontenjan Dolu") gösterilir ve sistem kullanıcıyı tekrar 3. adıma, yani ders bilgisi giriş ekranına yönlendirir. Bu sayede kullanıcı hatasını anında düzeltebilir.

Başarılı Ekleme: Eğer ders dört kontrolü de başarıyla geçerse, öğrencinin seçtiği dersler listesine eklenir ve toplam kredisi güncellenir.

Döngü Kararı: Ders başarıyla eklendikten sonra sistem kullanıcıya kritik soruyu sorar: "Başka Ders Eklemek İster misin?"

Evet: Kullanıcı "Evet" derse, akış tekrar 3. adıma (ders bilgisi giriş ekranı) döner ve döngü devam eder.

Hayır, Bitir: Kullanıcı "Hayır" derse, ders ekleme döngüsünden çıkılır ve kayıt sonlandırma sürecine geçilir.

Kayıt Özeti: Ekranda öğrencinin seçtiği tüm derslerin bir listesi ve toplam kredisi gösterilir.

Danışman Onayı Kontrolü: Öğrencinin genel not ortalaması (GPA) 2.5'in altında ise, kaydın geçerli olması için danışman onayı gerektiği belirtilir. Aksi takdirde, kaydın doğrudan tamamlandığı bilgisi verilir.

Bitiş: Kayıt işlemi sonlandırılır.
