# Portfolio Tasarım Rehberi — Futuristic Landing Page

## 1. Renk Paleti (Öneri)
| Rol | Renk | Kullanım Yeri |
|-----|------|---------------|
| Arka plan | `#0a0a0f` (koyu, hafif mavi alt tonlu) | Body |
| Metin | `#e0e0e0` (açık gri) | Paragraflar |
| Başlık | `#ffffff` | Ana başlıklar |
| Vurgu | `#4fc3f7` (soft neon mavi) veya `#b388ff` (lavanta moru) | Butonlar, linkler, glow |
| İkincil | `#1a1a2e` | Kart arka planları |

---

## 2. Section Sırası (HTML)

```
[ Navbar (sabit üstte) ]
[ Hero (karşılama)       ]  → 100vh, fade-in animasyonlu
[ About (kimim)          ]  → 2 sütun: metin + fotoğraf
[ Projects (projelerim)  ]  → grid kartlar
[ Certificates           ]  → kartlar veya yatay scroll
[ Languages (diller)     ]  → progress bar
[ Tech Stack             ]  → ikon/etiket grid
[ Contact (bana ulaşın)  ]  → form
[ Footer                 ]  → copyright + sosyal linkler
```

---

## 3. Kullanabileceğin Semantic HTML Etiketleri

| Etiket | Ne Zaman Kullanılır? |
|--------|---------------------|
| `<header>` | Navbar / logonun bulunduğu üst kısım |
| `<nav>` | Menü linklerini sarmak için |
| `<main>` | Sayfanın ana içeriği (hero'dan contact'a kadar) |
| `<section>` | Her bölümü gruplamak için (about, projects vb.) |
| `<article>` | Proje kartları gibi bağımsız içerikler |
| `<figure>` / `<figcaption>` | Görsel + alt yazı |
| `<h1> - <h6>` | Başlıklar (h1 sadece hero'da bir kere) |
| `<p>` | Paragraflar |
| `<ul>` / `<li>` | Menü öğeleri, tech stack listesi |
| `<a>` | Linkler (nav, butonlar) |
| `<button>` | CTA butonları |
| `<form>` | İletişim formu |
| `<input>` / `<textarea>` | Form alanları |
| `<footer>` | En alt bölüm |
| `<time>` | Tarih belirtirsen |

**Semantik kullanmanın avantajı:** SEO dostu, erişilebilir (screen reader uyumlu), kodun daha okunabilir.

---

## 4. CSS Teknikleri ve Nasıl Kullanılır

### 4.1. Flexbox (navbar, hero ortalamak, 2 sütunlu layout)
**Ne işe yarar:** Öğeleri yan yana veya alt alta dizer, hizalar.
**Kullanım:** Navbar'da linkleri yan yana dizmek, hero'da içeriği ortalamak, about bölümünde metin + görseli 2 sütun yapmak.
**Araştır:** `display: flex`, `justify-content`, `align-items`, `gap`, `flex-direction`

### 4.2. CSS Grid (proje kartları, tech stack)
**Ne işe yarar:** Tablo gibi satır/sütun bazlı dizilim.
**Kullanım:** Projeleri 3 kolonlu kart şeklinde dizmek, tech stack ikonlarını düzenli sıralamak.
**Araştır:** `display: grid`, `grid-template-columns: repeat(3, 1fr)`, `gap`

### 4.3. @keyframes Animasyonları (fade-in)
**Ne işe yarar:** CSS ile elementlerin zamanla değişmesini sağlar.
**Kullanım:** Hero başlığının yavaşça görünmesi (opacity 0 → 1, aşağıdan yukarı kayma).
**Araştır:**
```css
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(30px); }
  to   { opacity: 1; transform: translateY(0); }
}
.hero-title {
  animation: fadeInUp 1.2s ease forwards;
}
```

### 4.4. Smooth Scroll (yavaş sayfa geçişi)
**Ne işe yarar:** Linke tıklayınca sayfanın yumuşakça kayması.
**Kullanım:** Navbar'daki linkler "#about" gibi ID'lere giderken yavaş inmesi.
**Araştır:**
```css
html { scroll-behavior: smooth; }
```

### 4.5. Pseudo-element (nav dikey ayraç)
**Ne işe yarar:** HTML'e ekstra öğe yazmadan CSS'den çizgi/simge eklemek.
**Kullanım:** Menü linkleri arasına dikey çizgi.
**Araştır:**
```css
.nav-link::after {
  content: "|";
  margin: 0 15px;
  color: #555;
}
.nav-link:last-child::after {
  display: none;
}
```

### 4.6. Text-shadow / Box-shadow (glow/ışıma)
**Ne işe yarar:** Elemente dışarıya doğru yayılan ışıma efekti verir.
**Kullanım:** Başlıkta yumuşak bir ışıma, buton hover'ında glow.
**Araştır:**
```css
text-shadow: 0 0 20px rgba(79, 195, 247, 0.5);
box-shadow: 0 0 15px rgba(79, 195, 247, 0.3);
```

### 4.7. @media (responsiveness)
**Ne işe yarar:** Farklı ekran boyutlarına göre tasarımı uyarlamak.
**Kullanım:** Tablette 2 sütun, telefonda 1 sütun.
**Araştır:**
```css
@media (max-width: 768px) {
  .about { flex-direction: column; }
  .projects-grid { grid-template-columns: 1fr; }
}
```

### 4.8. CSS Variables (değişkenler)
**Ne işe yarar:** Renkleri tek bir yerden yönetmek.
**Araştır:**
```css
:root {
  --bg: #0a0a0f;
  --text: #e0e0e0;
  --accent: #4fc3f7;
}
body { background: var(--bg); color: var(--text); }
```

---

## 5. Navbar Tasarım Mantığı

```
┌─────────────────────────────────────┐
│ Logo    NavLink | NavLink | NavLink │
└─────────────────────────────────────┘
```

- Logo: `<a>` içinde `<img>` veya yazı
- NavLink: `<ul>` içinde `<li><a>`
- Dikey ayraçlar için: `::after` pseudo-element (yukarıda anlatıldı)
- Navbar sabit (fixed) olsun ki sayfa kayarken hep görünsün

---

## 6. Hero Bölümü Tasarım Mantığı

```
┌─────────────────────────────────────┐
│                                     │
│                                     │
│        ✦ Hoş Geldiniz ✦            │  ← h1, fadeInUp animasyonu
│     Bir cümlelik açıklama           │  ← p, biraz gecikmeli açılır
│         [ Keşfet ]                  │  ← button, en son açılır
│                                     │
└─────────────────────────────────────┘
```

- `height: 100vh` ile tam ekran
- `display: flex; justify-content: center; align-items: center` ile ortalama
- Animasyon sırası: başlık → paragraf → buton (animation-delay ile)

---

## 7. Bölümler Arası Geçiş İpucu

Her bölümün arka planını çok hafif değiştirebilirsin (ör: `#0a0a0f` ile `#0d0d1a` arasında gidip gelerek) ki kullanıcı sayfada aşağı indiğini hissetsin. Aşırı farklı olmasın, soft geçişler kullan.

---

## 8. Öğrenme Kaynakları

| Konu | Nereden Öğrenirim |
|------|-------------------|
| Flexbox | CSS Tricks "A Complete Guide to Flexbox" |
| CSS Grid | CSS Tricks "A Complete Guide to Grid" |
| @keyframes | MDN Web Docs "Using CSS Animations" |
| Pseudo-element | MDN "::after / ::before" |
| Smooth Scroll | MDN "scroll-behavior" |
| CSS Variables | MDN "Using CSS custom properties" |
| Semantic HTML | MDN "Semantic elements" |
| Responsive | MDN "Media queries" |
| Shadow/Glow | CSS Tricks "Almanac: box-shadow" |

Araştırma taktiği: Google'da `"CSS flexbox nedir"` veya `"CSS animations Türkçe"` diye arat. MDN Web Docs ve CSS Tricks en güvenilir kaynaklardır.

---

## 9. Çalışma Sırası (Öneri)

1. HTML iskeletini kur (semantic etiketlerle)
2. CSS ile renkleri ve genel görünümü ayarla
3. Navbar'ı yap (flex, ayraçlar, sabitleme)
4. Hero bölümünü yap (ortala, glow, fade-in)
5. Kalan bölümleri sırayla ekle (about, projects, cert, languages, tech, contact)
6. Smooth scroll ekle
7. Responsive yap (media queries)

Her bölümü tek tek hallet, sıradakine geçmeden bir öncekinden emin ol.
