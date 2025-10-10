FONKSIYON ATM_Calistir()

    // 1. Kart Girişi ve PIN Kontrolü
    KART_TAK()
    PIN_HATALI_DENEME = 0

    TEKRARLA:
        GIRILEN_PIN = PIN_ISTE()
        
        EĞER PIN_DOGRULA(GIRILEN_PIN) VEYA (PIN_HATALI_DENEME >= 3):
            DONGUYU_BITIR
        
        DEĞİLSE:
            PIN_HATALI_DENEME += 1
            
    SON_TEKRARLA

    // 2. Başarısız PIN Kontrolü
    EĞER PIN_HATALI_DENEME == 3:
        HATA_GOSTER("Kartınız bloke edilmiştir.")
        KART_IADE_ET()
        ISLEM_SONLANDIR()
        GERI_DON

    // 3. Ana İşlem Döngüsü
    DONGU_ANA_MENU:
        MENU_GOSTER("1: Bakiye Sorgula, 2: Para Çekme, 3: Çıkış")
        SECIM = KULLANICIDAN_AL()
        
        EĞER SECIM == 1:
            BAKIYE_GOSTER()
            
        DEĞİLSE EĞER SECIM == 2:
            Para_Cekme_Islemi()
            
        DEĞİLSE EĞER SECIM == 3:
            KART_IADE_ET()
            ISLEM_SONLANDIR()
            DONGUYU_BITIR
            
        // İşlem Sonrası Tekrar Sor (Döngü Koşulu)
        EĞER CEVAP_AL("Başka işlem yapmak ister misiniz? (E/H)") == 'H':
            KART_IADE_ET()
            DONGUYU_BITIR
    SON_DONGU
    
FONKSIYON Para_Cekme_Islemi()
    TUTAR = KULLANICIDAN_AL("Çekilecek tutarı giriniz:")
    
    // Koşul Kontrolü 1: 20 TL Katları
    EĞER TUTAR % 20 != 0:
        HATA_GOSTER("Hata: Tutar 20 TL'nin katları olmalıdır.")
        GERI_DON // Ana menüye dön
    
    // Koşul Kontrolü 2: Günlük Limit
    EĞER TUTAR > GUNLUK_LIMIT_KALAN:
        HATA_GOSTER("Hata: Günlük para çekme limitiniz aşıldı.")
        GERI_DON
    
    // Koşul Kontrolü 3: Yetersiz Bakiye
    EĞER TUTAR > HESAP_BAKIYESI:
        HATA_GOSTER("Hata: Yetersiz bakiye.")
        GERI_DON

    // Başarılı İşlem
    HESAP_BAKIYESI -= TUTAR
    GUNLUK_LIMIT_KALAN -= TUTAR
    PARA_VER(TUTAR)
    FIS_CIKAR("İşlem Başarılı.")

SON_FONKSIYON
