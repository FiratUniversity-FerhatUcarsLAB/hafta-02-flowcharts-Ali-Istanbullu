FONKSIYON ATM_ISLEM_AKISI()

    1. KART_GIRISI: Kartı al
    2. PIN_DENEME_SAYISI = 0

    DONGU_PIN_GIRISI (PIN_DENEME_SAYISI < 3 OLDUĞU SÜRECE):
        PIN_GIR: Kullanıcıdan PIN iste
        
        EĞER (PIN_DOGRU_MU(GİRİLEN_PIN)):
            Cikis_PIN_DONGUSU
        DEĞİLSE:
            PIN_DENEME_SAYISI = PIN_DENEME_SAYISI + 1
    SON_DONGU

    EĞER (PIN_DENEME_SAYISI == 3):
        KART_BLOKE_ET()
        KART_IADE_ET()
        ISLEM_BITIR()
        GERI_DON
    
    // PIN Doğrulandı, Ana İşlem Döngüsüne Geç
    DONGU_ANA_ISLEM (TRUE OLDUĞU SÜRECE):
        EKRANA_YAZ("Lütfen işlem seçiniz: 1. Para Çekme, 2. Bakiye Sorgulama, 3. Çıkış")
        SECIM = KULLANICIDAN_AL()

        EĞER (SECIM == 1): // Para Çekme
            TUTAR = KULLANICIDAN_AL("Çekmek istediğiniz tutarı giriniz:")
            
            // Koşul Kontrolleri
            EĞER (TUTAR % 20 != 0):
                EKRANA_YAZ("Hata: Tutar 20 TL'nin katları olmalıdır.")
                DEVAM_ET // Döngüye devam et, tekrar menüye dön
            
            EĞER (TUTAR > HESAP_BAKIYESI):
                EKRANA_YAZ("Hata: Yetersiz bakiye.")
                DEVAM_ET

            EĞER (TUTAR > GUNLUK_LIMIT):
                EKRANA_YAZ("Hata: Günlük limit aşıldı.")
                DEVAM_ET
            
            // Başarılı Çekme
            HESAP_BAKIYESI = HESAP_BAKIYESI - TUTAR
            PARA_VER(TUTAR)
            FİS_CIKAR("İşlem Başarılı: " + TUTAR + " TL")

        EĞER (SECIM == 2): // Bakiye Sorgulama
            EKRANA_YAZ("Hesap Bakiyeniz: " + HESAP_BAKIYESI + " TL")

        EĞER (SECIM == 3): // Çıkış
            EKRANA_YAZ("Kartınız iade ediliyor.")
            KART_IADE_ET()
            ISLEM_BITIR()
            GERI_DON

        // İşlem Sonrası Tekrar Sor (Asıl Döngü Sorusu)
        EKRANA_YAZ("Başka işlem yapmak ister misiniz? (E/H)")
        CEVAP = KULLANICIDAN_AL()
        
        EĞER (CEVAP == 'H'):
            Cikis_ANA_ISLEM_DONGUSU
    SON_DONGU
    
SON_FONKSIYON
