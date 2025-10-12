BAŞLA
    SÜREKLİ DÖNGÜ:
        // Hasta Kimlik Doğrulama
        EKRANA YAZDIR("Hastane Randevu ve Tahlil Sistemi")
        EKRANA YAZDIR("Lütfen TC Kimlik Numaranızı giriniz:")
        TC_KIMLIK_NO = KULLANICIDAN AL()

        EĞER (TC_KIMLIK_NO GEÇERLİ İSE)
            // Ana İşlem Seçimi
            EKRANA YAZDIR("Yapmak istediğiniz işlemi seçiniz:")
            EKRANA YAZDIR("1 - Randevu Al")
            EKRANA YAZDIR("2 - Tahlil Sonucu Görüntüle")
            ISLEM_SECIMI = KULLANICIDAN AL()

            EĞER (ISLEM_SECIMI EŞİTTİR 1)
                // Randevu Modülü
                EKRANA YAZDIR("Randevu Alma Modülü")
                SÜREKLİ DÖNGÜ (RANDEVU_DONGUSU):
                    POLIKLINIK = POLIKLINIK_SECIMI_AL()
                    DOKTOR_LISTESI = POLIKLINIK_DOKTORLARINI_GETIR(POLIKLINIK)
                    EKRANA YAZDIR("Lütfen bir doktor seçiniz:")
                    DOKTOR = KULLANICIDAN AL()

                    UYGUN_SAATLER = DOKTOR_UYGUN_SAATLERI_GETIR(DOKTOR)
                    EĞER (UYGUN_SAATLER BOŞ DEĞİL İSE)
                        EKRANA YAZDIR("Lütfen uygun bir saat seçiniz:")
                        SEÇİLEN_SAAT = KULLANICIDAN AL()

                        EKRANA YAZDIR("Randevu Onayı: [POLIKLINIK] - Dr. [DOKTOR] - [SEÇİLEN_SAAT]")
                        ONAY = KULLANICIDAN_ONAY_AL()

                        EĞER (ONAY EŞİTTİR EVET)
                            RANDEVU_KAYDET(TC_KIMLIK_NO, DOKTOR, SEÇİLEN_SAAT)
                            SMS_GONDER(TC_KIMLIK_NO, "Randevunuz başarıyla oluşturulmuştur.")
                            DÖNGÜDEN ÇIK (RANDEVU_DONGUSU) // Randevu başarılı, döngüden çık
                        AKSİ HALDE
                            EKRANA YAZDIR("Randevu onayı iptal edildi. Tekrar denemek ister misiniz?")
                            // Buraya tekrar deneme sorusu eklenebilir, şimdilik döngü devam etsin.
                    AKSİ HALDE
                        EKRANA YAZDIR("Seçilen doktor için uygun saat bulunmamaktadır.")
                        // Kullanıcıya farklı doktor veya poliklinik seçme imkanı sunulabilir
            
            AKSİ HALDE EĞER (ISLEM_SECIMI EŞİTTİR 2)
                // Tahlil Modülü
                EKRANA YAZDIR("Tahlil Sonucu Görüntüleme Modülü")
                
                TAHLIL_VAR_MI = TAHLIL_KONTROL(TC_KIMLIK_NO)
                EĞER (TAHLIL_VAR_MI EŞİTTİR EVET)
                    SONUC_HAZIR_MI = SONUC_HAZIRLIK_KONTROL(TC_KIMLIK_NO)
                    EĞER (SONUC_HAZIR_MI EŞİTTİR EVET)
                        TAHLIL_SONUCLARINI_GOSTER(TC_KIMLIK_NO)
                        EKRANA YAZDIR("1 - Sonuçları PDF İndir")
                        EKRANA YAZDIR("2 - Ana Menüye Dön")
                        SECIM_TAHLIL = KULLANICIDAN AL()
                        EĞER (SECIM_TAHLIL EŞİTTİR 1)
                            PDF_INDIR(TC_KIMLIK_NO)
                            EKRANA YAZDIR("PDF başarıyla indirildi.")
                    AKSİ HALDE
                        EKRANA YAZDIR("Tahlil sonuçlarınız henüz hazır değildir. Lütfen daha sonra tekrar deneyiniz.")
                AKSİ HALDE
                    EKRANA YAZDIR("Sistemde TC Kimlik Numaranıza ait tamamlanmış bir tahlil bulunmamaktadır.")

            AKSİ HALDE
                EKRANA YAZDIR("Geçersiz işlem seçimi.")
                
            // Başka İşlem Sorgusu
            EKRANA YAZDIR("Başka bir işlem yapmak ister misiniz? (E/H)")
            DEVAM = KULLANICIDAN AL()
            EĞER (DEVAM EŞİTTİR H)
                DÖNGÜDEN ÇIK (SÜREKLİ DÖNGÜ)
        AKSİ HALDE
            EKRANA YAZDIR("Geçersiz TC Kimlik Numarası. Lütfen tekrar deneyiniz.")
            
SON
