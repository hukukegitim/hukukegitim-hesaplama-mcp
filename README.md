# Hukuk Eğitim Hesaplama Araçları — MCP

[hukukegitim.com](https://hukukegitim.com/hesaplamaaraclari.aspx) üzerindeki hukuki hesaplama araçlarını yapay zekâ asistanlarına (Claude, ChatGPT, Cursor vb.) bağlayan **tek bir MCP sunucusu**.

Asistan tahmin yürütmek yerine hesabı doğrudan Hukuk Eğitim'in kendi hesaplayıcısına yaptırır; sonuç tarife sürümü, yasal dayanak ve notlarla birlikte gelir. Hesap mantığı sitede durur, bu depo yalnızca bağlantı bilgisini ve kullanım rehberini içerir.

> **Sunucu adresi:** `https://mcp.hukukegitim.com/hesaplama` (Streamable HTTP, giriş ve API anahtarı gerekmez)
>
> Hukuk Eğitim'in tüm MCP sunucularının listesi: [mcp.hukukegitim.com](https://mcp.hukukegitim.com)

> **Adres değişikliği:** Hesaplama sunucusu önce `https://hukukegitim.com/mcp`, ardından `https://hukukegitim.com/mcp/hesaplama` adresindeydi. Bu eski adresler şimdilik yeni adrese yönlendiriliyor (HTTP 307), mevcut bağlayıcılar çalışmaya devam eder; yine de **bağlayıcınızı `https://mcp.hukukegitim.com/hesaplama` ile güncelleyin.** Eski adresler ileride kaldırılacak.

## Araçlar

| Araç | Ne hesaplar | Durum |
|---|---|---|
| `vekalet-ucreti` | Avukatlık Asgari Ücret Tarifesi'ne (2025-2026) göre nispi/maktu vekalet ücreti | Yayında |
| `serbest-meslek-makbuzu` | Brüt–net, stopaj ve KDV dâhil/hariç dönüşümleri, makbuz kalemleri | Yayında |
| `arabuluculuk` | Arabuluculuk ücreti, makbuz ve dava şartı süreleri | Yakında |
| `iscilik-alacaklari` | Kıdem, ihbar, yıllık izin, fazla mesai, hafta tatili, UBGT; brüt–net maaş | Yakında |
| `tazminat` | Destekten yoksun kalma, sürekli/geçici iş göremezlik, bakıcı gideri | Yakında |
| `arac-deger-kaybi` | Araç değer kaybı | Yakında |
| `infaz` | Koşullu salıverilme, denetimli serbestlik, bihakkın tahliye tarihleri | Yakında |
| `zamanasimi` | Özel hukuk, ceza davası ve infaz zamanaşımı | Yakında |
| `mal-rejimi-tasfiyesi` | Edinilmiş mallara katılma rejiminde katılma alacağı ve değer artış payı | Yakında |

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
