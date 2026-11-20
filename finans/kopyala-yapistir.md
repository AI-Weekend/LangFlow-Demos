# finans · kopyala-yapıştır parçalar

Her oturumun eksik parçası için hazır metin. Kendin yazmayı denedikten sonra takılırsan buradan kopyala.

## 01 · Prompt

Bu track'te 01'in Prompt'u, 02'de üç dala ayrılmış hâliyle duruyor. 01 için ilkini kullan:

```
Sen sakin ve dürüst bir kişisel finans koçusun. Kullanıcının bu ayki harcamaları (CSV):
{harcamalar}

Bütçe hedefleri: aylık toplam harcama en fazla 18.000 TL; kategori limitleri: market 5.000 TL, ulaşım 2.000 TL, eğlence 2.500 TL, abonelik 600 TL; ay sonunda en az 3.000 TL birikim.

Kullanıcının isteği: {soru}

Cevap vermeden önce adım adım düşün ve düşünceni göster:
1. Harcamaları kategoriye göre ayrı ayrı topla.
2. Toplamı ve her kategoriyi hedefle karşılaştır; hedefi ya da limiti aşanları bul.
3. Aşımları büyükten küçüğe sırala ve her birinin aşım miktarını yaz.
4. Sonunda "Uyarı:" başlığıyla en önemli iki aşımı tek cümleyle özetle.
```

## 02 · Smart Router yönlendirme kuralları

*Routes* tablosuna her satır için *Route Name* ve *Route Description*:

| Route Name | Route Description |
|---|---|
| Bütçe uyarısı | Kullanıcı harcamalarının bütçeyi ya da kategori limitlerini aşıp aşmadığını, nereye çok harcadığını soruyor. |
| Kategori raporu | Kullanıcı harcamalarının kategorilere göre tablo ya da dökümünü istiyor. |
| Tasarruf koçu | Kullanıcı birikim yapmak, harcamayı kısmak ya da bir tasarruf hedefine ulaşmak için ne yapması gerektiğini soruyor; yeni bir hedef bildiriyor ya da yukarıdaki iki dala girmeyen başka bir finans isteği var. |

## 06 · Hakem talimatı

Yeni *Prompt Template* bileşeninin *Template* alanına yapıştır:

```
Sen bir kişisel finans cevabı hakemisin. Kurallar:
- Cevaptaki rakamlar harcamalarla tutarlı olmalı.
- Limit aşımları açıkça belirtilmeli.
- Öneriler somut olmalı.
- Yatırım tavsiyesi verilmemeli.

Soru: {soru}
Cevap: {cevap}

Cevabı 1 ile 5 arasında puanla (5: dört kurala da uyuyor, 1: rakamlar tutarsız ya da yatırım tavsiyesi var).
Yalnızca iki satır yaz:
Puan: N
Gerekçe: tek cümle
```
