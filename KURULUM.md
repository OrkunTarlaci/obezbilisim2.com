# Obez Bilişim – 3D Laptop Açılışı

## Kurulum (GitHub Pages, build gerekmez)
Bu klasördeki dosyaları repo köküne kopyala:

| Dosya | Durum |
|---|---|
| `index.html` | Mevcut dosyanın yerine geçer. Orijinalden **hiçbir satır silinmedi**; `<head>` içine 44 satır eklendi. |
| `intro/obez-intro.js` | Yeni (~28 KB, bağımlılıksız, WebGL2) |
| `intro/laptop.glb` | Yeni (162 KB; orijinal 700 KB) |

Yeni kütüphane/npm/build yok. `CNAME`, `sitemap.xml`, `siteler/` ve diğer dosyalara dokunulmadı.

## Nasıl çalışır
- Ekran quad'ı canvas'ta "delik" bırakılır; altında gerçek site (`index.html?embed=1`, iframe) tek bir `matrix3d` ile kamerayla aynı perspektifte çalışır. Çerçeve, çentik, menteşe modelin kendi geometrisidir.
- Kapak, modelin **kapanma klibinin anahtarları tersten okunarak** açılır (zamanlama yumuşatılmıştır). Pivot menteşe düğümüdür.
- Kamera ekranı tam doldurunca overlay kalkar; kullanıcı **gerçek sayfada** kalır (gerçek URL, SEO, formlar, analitik). Son kare gerçek sayfadan piksel piksel ayırt edilemez (test: 4 pencere oranında ortalama fark ≤0,0002/255).

## Ne zaman oynar
Oturumda **bir kez**, yalnızca ana sayfada. Oynamaz: mobil/dikey/<900px, dokunmatik tablet, `prefers-reduced-motion`, veri tasarrufu, ≤2 GB RAM / ≤2 çekirdek, WebGL2 yok, `#bölüm` bağlantıları, iframe içinde. Model/WebGL hata verirse ya da 15 sn'de hazır olmazsa site doğrudan açılır. Yavaş cihazda ilk 40 karede performans düşükse çözünürlük düşürülür, yine yetmezse atlanır.
Kullanıcı "Animasyonu geç" düğmesi veya **Esc** ile atlayabilir. Animasyon sırasında ana sayfa kaydırması kilitli ve klavyeye kapalıdır (`inert`); bitince/atlayınca serbest bırakılır.

## URL parametreleri
`?intro=1` zorla oynat (koşulları yok sayar) · `?intro=0` kapat · `?introdebug=1` geliştirici: `obezIntroDebug.seek(saniye)` ile kare kare inceleme.

## Ayarlar (`intro/obez-intro.js`, en üst)
`T` nesnesi: süreler (kapak, ekran uyanma, yaklaşma, toplam ≈5,75 sn). Oturum yerine her ziyarette oynatmak için `index.html` içindeki `sessionStorage` kontrolünü kaldır.

## Dikkat
- Repoda `siteler/Obez-Bili-im-main/` altında tüm sitenin **kopyası** ve kökte uzantısız `Obez Bilişim` dosyası var. Dokunulmadı; yayında kullanılmıyorsa silmeyi düşünebilirsin (zip'in 77 MB olmasının nedeni).
- Sitede SEO `meta description`/Open Graph etiketi yok (orijinalde de yoktu); istersen ayrıca ekleyebilirim.
