BAŞLA

Kart takılır
PIN_giris_hak = 3

TEKRAR:
    PIN sor
    eğer PIN doğru ise
        bakiye_sorgula()
        GİT İŞLEM
    değilse
        PIN_giris_hak = PIN_giris_hak - 1
        eğer PIN_giris_hak == 0 ise
            "Kart bloke edildi!" yazdır
            BİTİR
        değilse
            "Hatalı PIN, tekrar deneyin" yazdır
            GİT TEKRAR

İŞLEM:
    bakiye = hesap_bakiyesi
    PARA_CEKME:

        tutar = kullanıcıdan_tutar_al()

        eğer tutar > bakiye ise
            "Yetersiz bakiye!" yazdır
            GİT PARA_CEKME

        eğer tutar % 20 ≠ 0 ise
            "Tutar 20 TL’nin katı olmalı!" yazdır
            GİT PARA_CEKME

        eğer tutar > günlük_limit ise
            "Günlük limit aşıldı!" yazdır
            GİT PARA_CEKME

        bakiye = bakiye - tutar
        "Para veriliyor..." yazdır
        "Fiş çıkarılıyor..." yazdır

        BAŞKA_ISLEM:
            "Başka işlem yapmak ister misiniz? (E/H)" yazdır
            cevap = al()

            eğer cevap == 'E' ise
                GİT İŞLEM
            değilse
                "Kart iade edildi." yazdır
                BİTİR

SON_FONKSIYON
