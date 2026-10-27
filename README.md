# Hukuk Eğitim Hesaplama Araçları — MCP

[hukukegitim.com](https://hukukegitim.com/hesaplamaaraclari.aspx) üzerindeki hukuki hesaplama araçlarını yapay zekâ asistanlarına (Claude, ChatGPT, Cursor vb.) bağlayan **tek bir MCP sunucusu**.

Asistan tahmin yürütmek yerine hesabı doğrudan Hukuk Eğitim'in kendi hesaplayıcısına yaptırır; sonuç tarife sürümü, yasal dayanak ve notlarla birlikte gelir. Hesap mantığı Hukuk Eğitim'in sunucusunda çalışır; bu depo yalnızca bağlantı bilgisini ve kullanım rehberini içerir.

> **Sunucu adresi:** `https://mcp.hukukegitim.com/hesaplama` (Streamable HTTP, giriş ve API anahtarı gerekmez)
>
> Hukuk Eğitim'in tüm MCP sunucularının listesi: [mcp.hukukegitim.com](https://mcp.hukukegitim.com)

> **Adres değişikliği:** Hesaplama sunucusu önce `https://hukukegitim.com/mcp`, ardından `https://hukukegitim.com/mcp/hesaplama` adresindeydi. Bu eski adresler şimdilik yeni adrese yönlendiriliyor (HTTP 307), mevcut bağlayıcılar çalışmaya devam eder; yine de **bağlayıcınızı `https://mcp.hukukegitim.com/hesaplama` ile güncelleyin.** Eski adresler ileride kaldırılacak.

## Araçlar

Şu an **18 araç** yayında:

| Araç | Ne hesaplar |
|---|---|
| `vekalet-ucreti` | Avukatlık Asgari Ücret Tarifesi'ne (2025-2026) göre nispi/maktu vekalet ücreti |
| `serbest-meslek-makbuzu` | Brüt–net, stopaj ve KDV dâhil/hariç dönüşümleri, makbuz kalemleri |
| `iscilik-alacaklari` | Kıdem ve ihbar tazminatı, yıllık izin, fazla mesai, hafta tatili, UBGT; brüt ve net (SGK, vergi, damga, asgari ücret istisnası) |
| `maas-brut-net` | Aylık bordro: brütten nete veya netten brüte maaş (SGK, işsizlik, gelir ve damga vergisi) |
| `arac-deger-kaybi` | Araç değer kaybı (1 Temmuz 2026 öncesi mülga Ek-1 formülü, sonrası ikinci el değer farkı) |
| `infaz-yatar` | Koşullu salıverilme, denetimli serbestlik ve bihakkın tahliye tarihleri |
| `mal-rejimi-tasfiyesi` | Edinilmiş mallara katılma rejiminde katılma alacağı ve takas |
| `mal-rejimi-deger-artis-payi` | Edinilmiş mallara katılma rejiminde değer artış payı |
| `arabuluculuk-ucreti` | Arabuluculuk ücreti (2026 tarifesi: nispi, saat ücreti, seri ve kira uyuşmazlıkları, taraf payı) |
| `arabuluculuk-makbuz` | Arabuluculuk serbest meslek makbuzu dökümü |
| `arabuluculuk-sureler` | Dava şartı arabuluculukta süreler ve son tarihler |
| `zamanasimi-ozel-hukuk` | Özel hukukta zamanaşımı (kesilme ve durma ile) |
| `zamanasimi-ceza-dava` | Ceza davası zamanaşımı |
| `zamanasimi-ceza-infaz` | Ceza infaz zamanaşımı |
| `tazminat-destekten-yoksun-kalma` | Ölüm: destekten yoksun kalma tazminatı |
| `tazminat-surekli-is-goremezlik` | Sürekli iş göremezlik tazminatı |
| `tazminat-gecici-is-goremezlik` | Geçici iş göremezlik tazminatı |
| `tazminat-bakici-gideri` | Bakıcı gideri tazminatı |

Yeni araçlar eklendikçe sunucunun araç listesinde kendiliğinden görünür; bağlantıyı yeniden kurmanız gerekmez. Güncel liste için asistanınızdan araçları listelemesini isteyin.

## Kurulum

**Claude:** Ayarlar → Bağlayıcılar → Özel bağlayıcı ekle → adres olarak `https://mcp.hukukegitim.com/hesaplama` girin. Kimlik doğrulama yok.

**ChatGPT:** Geliştirici modunda yeni bağlayıcı ekleyin → adres `https://mcp.hukukegitim.com/hesaplama`, kimlik doğrulama "Yok".

**Claude Code:**

```bash
claude mcp add --transport http hukukegitim-hesaplama https://mcp.hukukegitim.com/hesaplama
```

## Deneyin

| Soru | Beklenen sonuç |
|---|---|
| "2,5 milyon TL'lik asliye davasında vekalet ücreti ne olur?" | 367.000 TL |
| "Net 12.345,67 TL KDV hariç makbuz kes, stopaj %20, KDV %20" | KDV dâhil brüt 18.518,51 TL |
| "Haziranda 45.000 TL brüt maaşın neti ne kadar?" | 34.720,48 TL |

## Girdi kuralları

- Tutarlar **sayı** olarak gönderilir (`60000.5`). `60.000,50 TL` biçimi kabul edilmez; asistan bunu sizin yerinize dönüştürür.
- Tarihler `YYYY-AA-GG` biçimindedir.
- Hatalı girdide araç hangi alanın neden reddedildiğini Türkçe bildirir.
- Her cevapta kısa bir `ozet` ve sitedeki ayrıntılı hesap sayfasının bağlantısı (`kaynak`) da bulunur.

## Sınırlar

IP başına dakikada 300 istek. Sorun yaşarsanız saatiyle birlikte bildirin.

## Önemli not

Sonuçlar **bilgilendirme amaçlıdır**, hukuki görüş değildir. Her cevapta hangi tarife sürümüne göre hesaplandığı ve yasal dayanak belirtilir; resmî işlemlerde kendi kontrolünüzü yapın.

## Araç sayfaları

Her aracın ayrıntılı, görsel arayüzlü sürümü sitede: [hukukegitim.com/hesaplamaaraclari.aspx](https://hukukegitim.com/hesaplamaaraclari.aspx). Orada sonuçları dava dosyanıza da kaydedebilirsiniz.

## Lisans

Bu depodaki dokümantasyon [MIT](LICENSE) lisanslıdır. Hesaplama araçları ve verileri Hukuk Eğitim'e aittir.
