Başla

SistemAktifMi = sor("Sistem aktif mi?")
Eğer SistemAktifMi == Hayır:
    uyar("Sistem aktif değil!")
    Bitir

GeceMi = sor("Gece mi? Gündüz mü?")
Eğer GeceMi == Gece:
    GeceGorusAc()
Eğer GeceMi == Gündüz:
    GünduzModu()

Sonsuz Döngü Başla:

    EvSahibiEvdeMi = sor("Ev sahibi evde mi?")
    
    Eğer EvSahibiEvdeMi == Evet:
        # Ev sahibi evdeyse sensörleri yine kontrol et
        HareketVar = HareketSensoruOku()
        Isı = IsıSensoruOku()
        Eğer HareketVar ve Isı > 30:
            # İnsan var → Seviye 1 alarm
            Seviye1Alarm()
            BildirimGonder()
        BekleVeTekrarKontrolEt()

    Eğer EvSahibiEvdeMi == Hayır:
        # Ev sahibi yoksa sensör döngüsü
        HareketVar = HareketSensoruOku()
        Eğer HareketVar == Hayır:
            BekleVeTekrarKontrolEt()
            Devam

        Isı = IsıSensoruOku()
        Eğer Isı <= 30:
            # Hayvan veya nesne → alarm yok
            BekleVeTekrarKontrolEt()
            Devam

        # İnsan var → yüz tanıma
        YuzDurumu = YuzTanima()
        
        Eğer YuzDurumu == Tanıdık:
            Seviye1Alarm()
            BildirimGonder()
        
        Eğer YuzDurumu == Taninmadik:
            Seviye2Alarm()  # Kamera + Uyarı + Kapılar ve Pencereler kilitlensin
            BildirimGonder()
        
        Eğer YuzDurumu == Maskeli:
            EveGirdiMi = EveGirisKontrol()
            Eğer EveGirdiMi == Hayır:
                Seviye3Alarm()  # Kamera + Uyarı + Kapılar/Pencereler kilitlensin
                BildirimGonder()
            Eğer EveGirdiMi == Evet:
                Seviye3SisAlarm()  # Sis sistemi çalıştır + Kapılar/Pencereler zaten kilitli
                BildirimGonder()
    
    BekleVeTekrarKontrolEt()

Sonsuz Döngü Sonu

