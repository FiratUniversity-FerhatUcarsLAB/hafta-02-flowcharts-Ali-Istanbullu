BASLA OnlineAlisverisSistemi

    // A1, A2, A3: Kullanıcı Girişi Kontrolü
    DOGRULANDI = YANLIS
    IKEN (DOGRULANDI == YANLIS) DO
        KULLANICI_GIRISI = KULLANICI_GIRISI_AL()
        DOGRULANDI = KULLANICI_GIRIS_KONTROLU(KULLANICI_GIRISI)
        EGER (DOGRULANDI == YANLIS) O ZAMAN
            EKRANA_YAZ "Hatalı Giriş. Tekrar Deneyin."
        SON
    SON

    // B1 - B6: Ürün Gezinme ve Sepete Ekleme Döngüsü
    TEKRAR_ALISVERIS_ET: // <-- Stok ve Min 50 TL kontrolünden buraya dönülür (B1)
    DEVAM_ET = DOGRU
    IKEN (DEVAM_ET == DOGRU) DO
        EKRANA_YAZ "Ürün Kategorilerini Listele..."
        ... (Kategori ve Ürün Seçimi) ...
        MIKTAR = MIKTAR_GIRISI_AL()

        // B3: Stok Kontrolü
        EGER (STOK_KONTROL(URUN_SECIMI, MIKTAR) == DOGRU) O ZAMAN
            SEPETE_EKLE(URUN_SECIMI, MIKTAR) // B4
            EKRANA_YAZ "Ürün sepete eklendi."
        DIGER DURUMDA
            EKRANA_YAZ "Yetersiz Stok! Yeni seçim için yönlendiriliyor." // B5
            GIT TEKRAR_ALISVERIS_ET // B1'e dön
        SON

        EKRANA_YAZ "Alışverişe Devam Etmek İster Misiniz? (E/H)"
        EGER (KULLANICI_CEVABI_AL() == 'H') O ZAMAN // B6
            DEVAM_ET = YANLIS
        SON
    SON

    // C1, C2: Sepeti Görüntüleme ve Düzenleme Döngüsü
    SEPET_DUZENLE = DOGRU
    IKEN (SEPET_DUZENLE == DOGRU) DO
        SEPETI_GORUNTULE()
        ... (Düzenleme işlemleri) ...
        EGER (Kullanıcı 'Devam Et' dedi) O ZAMAN
            SEPET_DUZENLE = YANLIS
        SON
    SON

    SEPET_TOPLAMI = SEPET_TUTARI_HESAPLA()

    // C3: Minimum Tutar Kontrolü
    EGER (SEPET_TOPLAMI < 50.00) O ZAMAN // Koşul
        EKRANA_YAZ "Siparişi tamamlamak için minimum tutar (50 TL) sağlanamadı. Ürün eklemeye yönlendiriliyor."
        GIT TEKRAR_ALISVERIS_ET // B1'e dön
    SON

    // D1 - D3: İndirim Kodu Uygulama
    EGER (INDIM_KODU_GIRILDI == DOGRU) O ZAMAN // D1
        KOD = KOD_GIRISI_AL()
        EGER (KOD_GECERLI_MI(KOD) == DOGRU) O ZAMAN
            SEPET_TOPLAMI = INDIRIMI_UYGULA(SEPET_TOPLAMI, KOD) // D2
        DIGER DURUMDA
            EKRANA_YAZ "Geçersiz İndirim Kodu." // D3
        SON
    SON

    // D4 - D6: Kargo Ücreti Hesaplama
    KARGO_UCRETI = 15.00
    EGER (SEPET_TOPLAMI > 200.00) O ZAMAN // D4
        KARGO_UCRETI = 0.00 // D5
    DIGER DURUMDA
        // D6
    SON
    TOPLAM_ODENECEK = SEPET_TOPLAMI + KARGO_UCRETI

    // E1, E2: Ödeme Yöntemi Seçimi
    ODEME_SECIMI_YAPILDI = YANLIS
    IKEN (ODEME_SECIMI_YAPILDI == YANLIS) DO
        ODEME_YONTEMI = KULLANICI_SECIMI_AL()
        EGER (ODEME_YONTEMI_GECERLI_MI(ODEME_YONTEMI) == DOGRU) O ZAMAN // E1
            ODEME_SECIMI_YAPILDI = DOGRU
        DIGER DURUMDA
            EKRANA_YAZ "Geçersiz ödeme yöntemi." // E2
        SON
    SON

    // E3, E4, E5: Sipariş Onayı
    EKRANA_YAZ "Toplam Ödenecek Tutar: " + TOPLAM_ODENECEK + " TL"
    EKRANA_YAZ "Siparişi Onaylıyor Musunuz? (E/H)"
    EGER (KULLANICI_CEVABI_AL() == 'E') O ZAMAN // E3
        SIPARISI_OLUSTUR(SEPET, TOPLAM_ODENECEK, ODEME_YONTEMI) // E4
        EKRANA_YAZ "Siparişiniz Başarıyla Oluşturuldu!"
    DIGER DURUMDA
        EKRANA_YAZ "Sipariş İptal Edildi." // E5
    SON

BIT OnlineAlisverisSistemi
