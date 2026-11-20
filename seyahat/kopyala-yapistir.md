# seyahat · kopyala-yapıştır parçalar

Her oturumun eksik parçası için hazır metin. Kendin yazmayı denedikten sonra takılırsan buradan kopyala.

## 01 · Prompt

*Prompt Template* bileşeninin *Template* alanına yapıştır:

```
Sen deneyimli bir seyahat danışmanısın. Kullanıcının gezi isteği:
{gezi_istegi}

Cevap vermeden önce adım adım düşün ve düşünceni göster:
1. İsteği özetle: nereye, ne zaman, kaç gün, kaç kişi, bütçe ipucu var mı?
2. Rota: ulaşım ve konaklama bölgesi için 2 seçeneği kısaca karşılaştır, birini seç ve nedenini tek cümleyle yaz.
3. Bütçe: uçak, konaklama, yemek, şehir içi ulaşım ve aktiviteler için kalem kalem tahmini tutar yaz.
4. Belge kontrol listesi: pasaport (Schengen çıkışından sonra en az 3 ay geçerli olmalı), vize, sigorta ve rezervasyonlar için yapılacakları maddele.
5. Gün gün program: her güne sabah, öğleden sonra ve akşam için birer öneri yaz.

Güncel fiyat ya da vize ücreti gibi emin olmadığın bilgiyi kesinmiş gibi yazma; "Tahmini:" diye belirt.
```

## 02 · Smart Router yönlendirme kuralları

*Routes* tablosuna her satır için *Route Name* ve *Route Description*:

| Route Name | Route Description |
|---|---|
| Gezi planı | Kullanıcı gezi planı istiyor: nereye gidileceği, gezilecek yerler, rota, gün gün program; ya da gezi tercihlerini anlatıyor (yalnız gitmek, kalabalıktan kaçınmak, tempo). Örnek: Lizbon için 3 günlük program yap. |
| Bütçe ve belgeler | Kullanıcı gezinin parasını ya da evraklarını soruyor: tahmini maliyet, bütçe toplamı, vize, pasaport, sigorta, hangi belgeler gerekli, belgelerim yeterli mi. Örnek: Pasaportum yeterli mi? Toplam kaç euro tutar? |

## 06 · Hakem talimatı

Yeni *Prompt Template* bileşeninin *Template* alanına yapıştır:

```
Sen bir seyahat hazırlığı hakemisin. Kural:
- Pasaport, Schengen bölgesinden planlanan çıkıştan sonra en az 3 ay geçerli olmalı. Pasaport gezi tarihinden önce bitiyorsa ya da bu süreyi karşılamıyorsa cevap bunu açıkça uyarmalı.

Soru: {soru}
Cevap: {cevap}

Cevabı 1 ile 5 arasında puanla (5: pasaport kuralı doğru uygulanmış, 1: geçersiz pasaport uyarısız geçilmiş).
Yalnızca iki satır yaz:
Puan: N
Gerekçe: tek cümle
```
