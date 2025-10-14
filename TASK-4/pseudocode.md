BAŞLA

  // --- Değişken Tanımlamaları ---
  ogrenci_girisi_basarili = FALSE
  secilen_dersler = []
  toplam_kredi = 0
  KREDI_LIMITI = 35

  // --- 1. Öğrenci Girişi Döngüsü ---
  DÖNGÜ (ogrenci_girisi_basarili == FALSE iken):
    YAZ "Öğrenci numaranızı giriniz:"
    OKU ogrenci_no
    YAZ "Şifrenizi giriniz:"
    OKU sifre
    EĞER (ogrenci_no + sifre) veritabanında DOĞRU İSE
      ogrenci_girisi_basarili = TRUE
      ogrenci_bilgileri = veritabanından_ogrenci_bilgilerini_al(ogrenci_no)
    DEĞİLSE
      YAZ "Hatalı giriş. Lütfen tekrar deneyin."
    SON EĞER
  SON DÖNGÜ

  // --- 2. Ders Listesini Gösterme ---
  YAZ "--- Seçilebilecek Dersler ---"
  sistemdeki_dersleri_goster()

  // --- 3. Ana Ders Ekleme Döngüsü ---
  DÖNGÜ (TRUE): // Bu döngüden sadece kullanıcı isteğiyle çıkılır
    YAZ "Eklemek istediğiniz dersin kodunu girin:"
    OKU eklenecek_ders_kodu
    eklenecek_ders = sistemdeki_dersler arasından bul(eklenecek_ders_kodu)

    // Kontroller
    EĞER eklenecek_ders.kontenjan_dolu() İSE
      YAZ "HATA: Dersin kontenjanı dolu."
      DEVAM ET // Döngünün başına dön
    SON EĞER

    EĞER ogrenci_on_kosulu_saglamiyor(eklenecek_ders) İSE
      YAZ "HATA: Bu dersin ön koşulunu sağlamıyorsunuz."
      DEVAM ET // Döngünün başına dön
    SON EĞER

    EĞER zaman_cakismasi_var(eklenecek_ders, secilen_dersler) İSE
      YAZ "HATA: Seçtiğiniz başka bir ders ile zaman çakışması var."
      DEVAM ET // Döngünün başına dön
    SON EĞER

    EĞER (toplam_kredi + eklenecek_ders.kredisi) > KREDI_LIMITI İSE
      YAZ "HATA: Kredi limitini (35) aşıyorsunuz."
      DEVAM ET // Döngünün başına dön
    SON EĞER

    // Başarılı Ekleme
    secilen_dersler listesine eklenecek_ders'i ekle
    toplam_kredi = toplam_kredi + eklenecek_ders.kredisi
    YAZ eklenecek_ders.adi, " dersi başarıyla eklendi."

    // Döngü Kararı
    YAZ "Başka ders eklemek ister misiniz? (E/H)"
    OKU devam_et_secimi
    EĞER devam_et_secimi == 'H' VEYA devam_et_secimi == 'h' İSE
      DÖNGÜDEN ÇIK // Ana döngüyü sonlandır
    SON EĞER
  SON DÖNGÜ

  // --- 4. Kayıt Özeti ve Sonlandırma ---
  YAZ "\n--- Kayıt Özeti ---"
  HER ders İÇİN secilen_dersler:
    YAZ ders.kodu, ders.adi, ders.kredisi
  SON HER
  YAZ "Toplam Kredi:", toplam_kredi

  // Danışman Onayı Kontrolü
  EĞER ogrenci_bilgileri.GPA < 2.5 İSE
    YAZ "UYARI: Not ortalamanız 2.5'in altında olduğu için kaydınızın danışman tarafından onaylanması gerekmektedir."
  DEĞİLSE
    YAZ "Kaydınız başarıyla tamamlanmıştır."
  SON EĞER

  kayit_bilgilerini_veritabanına_gonder(secilen_dersler)

BİTİR
