# mutfak · kopyala-yapıştır parçalar

Her oturumun eksik parçası için hazır metin. Kendin yazmayı denedikten sonra takılırsan buradan kopyala.

## 01 · Prompt

*Prompt Template* bileşeninin *Template* alanına yapıştır:

```
Sen pratik bir ev aşçısısın. Kullanıcının elindeki malzemeler:
{malzemeler}

Cevap vermeden önce adım adım düşün ve düşünceni göster:
1. Malzemeleri listele; hangisi ana malzeme olabilir?
2. Bu malzemelerle yapılabilecek 2-3 yemek fikrini kısaca karşılaştır.
3. En uygun olanı seç ve nedenini tek cümleyle açıkla.
4. Seçtiğin tarifi malzeme listesi ve numaralı adımlarla yaz.

Evde olmayan bir malzeme gerekiyorsa en sonda "Eksik:" başlığıyla ayrıca belirt.
```

## 02 · Smart Router yönlendirme kuralları

*Routes* tablosuna her satır için *Route Name* ve *Route Description*:

| Route Name | Route Description |
|---|---|
| Tarif | Kullanıcı elindeki malzemelerle ne pişirebileceğini, bir yemeğin nasıl yapıldığını, ne pişirmesi gerektiğine dair öneri ya da tarif defterindeki bir tarifin malzemesini veya alerjenini soruyor. |
| Alışveriş listesi | Kullanıcı bir yemek ya da menü için neler alması gerektiğini, alışveriş listesini istiyor. |
| Beslenme | Kullanıcı kalori, protein, vitamin gibi besin değerlerini soruyor, bir yemeğin sağlıklı olup olmadığını soruyor ya da kendi diyetini, alerjisini veya beslenme kısıtını anlatıyor. |

## 06 · Hakem talimatı

Yeni *Prompt Template* bileşeninin *Template* alanına yapıştır:

```
Sen bir mutfak hakemisin. Evin kuralları:
- Kuzen Elif'in yer fıstığı ve Antep fıstığı alerjisi var; bunları içeren bir tarif uyarısız önerilmemeli.
- Babam gluteni azaltıyor; aynı cevapta birden fazla börek ya da hamur işi olmamalı.

Soru: {soru}
Cevap: {cevap}

Cevabı 1 ile 5 arasında puanla (5: kurallara tam uyuyor, 1: fıstıklı tarif uyarısız önerilmiş).
Yalnızca iki satır yaz:
Puan: N
Gerekçe: tek cümle
```
