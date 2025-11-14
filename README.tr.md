### Middleman projeleri için Hızlı ve Akıllı CSS/SCSS kodlama kütüphanesi v2.1.4

**Türkçe** | **[English](README.md)**

![Cross-Browser-Support](https://cloud.githubusercontent.com/assets/6649597/14348854/c04152a0-fcc7-11e5-9e5f-035d3a683d85.png)


## Genel Bakış

**Agile CSS Framework**, Ruby tabanlı Middleman statik site oluşturucu için tasarlanmış güçlü ve esnek bir SASS/SCSS mixin kütüphanesidir. Bu framework, modern web geliştirme sürecinizi hızlandırmak ve kodunuzu daha okunabilir, yeniden kullanılabilir hale getirmek için tasarlanmıştır.

### Neden Bu Kütüphane?

- **Middleman İçin Optimize Edilmiş**: Ruby Middleman projelerinde sorunsuz çalışır
- **Responsive Grid Sistemi**: Bootstrap uyumlu 12 kolonlu grid sistemi dahil
- **Cross-Browser Desteği**: Tüm modern tarayıcılarda sorunsuz çalışır
- **Hazır UI Bileşenleri**: Navigation, dropdown, tooltip ve daha fazlası
- **CSS3 Mixin'ler**: Animation, transition, transform ve modern CSS özellikleri
- **FontAwesome Entegrasyonu**: 693 adet hazır ikon

Versiyon
----

2.1.4


## Kurulum

### Middleman Projesine Kurulum

1. **Kütüphaneyi projenize ekleyin:**

   ```bash
   # Proje kök dizininde
   git clone https://github.com/ozbilgic/agile-css-framework-for-middleman.git vendor/agile-css
   # veya indirip vendor klasörüne çıkartın
   ```

2. **Middleman config.rb dosyanızı güncelleyin:**

   ```ruby
   # config.rb
   configure :build do
     activate :minify_css
     activate :minify_javascript
   end

   # SCSS için yol ekleyin
   config[:sass_assets_paths] << File.join(root, 'vendor/agile-css')
   ```

3. **Ana SCSS dosyanıza import edin:**

   ```scss
   // source/stylesheets/site.css.scss

   @import "agile.css.scss";

   // Veya sadece grid sistemi için:
   @import "src/grid12";

   // Kendi stilleriniz
   .my-custom-class {
     @include border-radius(10px);
   }
   ```

4. **Layout dosyanızda CSS'i dahil edin:**

   ```erb
   <!-- source/layouts/layout.erb -->
   <!doctype html>
   <html>
     <head>
       <%= stylesheet_link_tag :site %>
     </head>
     <body>
       <%= yield %>
     </body>
   </html>
   ```


## Temel Kullanım

### Grid Sistemi Kullanımı

```html
<div class="container">
  <div class="row">
    <div class="col-md-4">Kolon 1</div>
    <div class="col-md-4">Kolon 2</div>
    <div class="col-md-4">Kolon 3</div>
  </div>
</div>
```

### Mixin Kullanımı

```scss
.my-button {
  padding: 10px 20px;
  background: #3498db;
  color: white;

  @include border-radius(5px);
  @include transition(all 0.3s ease);
  @include boshadow(0 2px 5px rgba(0,0,0,0.2));

  &:hover {
    @include transform2d(translateY(-2px));
    @include boshadow(0 4px 8px rgba(0,0,0,0.3));
  }

  // Mobil için
  @include media($tablet) {
    padding: 8px 16px;
    font-size: 14px;
  }
}
```

### Responsive Navigation Örneği

```scss
#main-nav {
  @include horizontal-navbar(
    $bgColor: #2c3e50,
    $textColor: white,
    $hoverBgColor: #34495e,
    $activeLinkBgColor: #3498db
  );
}
```


## Middleman Helper'ları ile Entegrasyon

```ruby
# config.rb - Yardımcı metodlar
helpers do
  def grid_column(size, content, options = {})
    classes = ["col-md-#{size}"]
    classes << options[:extra_class] if options[:extra_class]
    content_tag :div, content, class: classes.join(' ')
  end
end
```

```erb
<!-- Kullanım -->
<%= grid_column(4, "İçerik", extra_class: "my-class") %>
```


Özellikler
----
* **Fonksiyonlar »**

Açıklama | Özellik
------------ | -------------
» [Pixel'i "em" formatına dönüştürür.](#-pixel-converts-the-em-format) | <ul><li>**@function convert_em()**</li><li>*Belirtilen "px" değerini "em" formatına dönüştürür.*</li></ul>

* **Mixin'ler »**

Açıklama | Özellik
------------ | -------------
» [CSS3 Prefix Ekleme.](#-css3-prefix-adding) | <ul><li>**@mixin prefix()**</li><li>*Tarayıcı özellikleri için destek ekler.*</li></ul>
» [Responsive Media Seçici.](#-responsive-media-selector) | <ul><li>**@mixin media()**</li><li>*Belirli ekran çözünürlükleri için kod ekler.*</li></ul>
» [Alternatif Responsive Media Seçici.](#-alternate-responsive-media-selector) | <ul><li>**@mixin media-query()**</li><li>*Farklı ekran çözünürlükleri için kod ekler.*</li></ul>
» [Elementler için Alpha Kanalı Ayarlama. Cross Browser Destekli.](#-setting-the-alpha-channel-for-items) | <ul><li>**@mixin opacity()**</li><li>*Elementlere alpha kanalı ekler.*</li></ul>
» [Border Radius Ayarlama.](#-set-border-radius) | <ul><li>**@mixin border-radius()**</li><li>*Border radius ekler.*</li></ul>
» [Kısa Animasyon Ayarlama.](#-set-shorthand-animation) | <ul><li>**@mixin animation()**</li><li>*Animasyon adı ve özellikleri girmenizi sağlar.*</li></ul>
» [Animasyon Oluşturucu.](#-animation-creator) | <ul><li>**@mixin keyframes()**</li><li>*Yeni bir animasyon tanımlamanızı sağlar.*</li></ul>
» [Geçiş Efekti.](#-transition) | <ul><li>**@mixin transition()**</li><li>*Özellik değerlerini belirli bir sürede düzgünce değiştirmenizi sağlar.*</li></ul>
» [2D Dönüşümler.](#-2d-transforms) | <ul><li>**@mixin transform2d()**</li><li>*Elementleri çevirme, döndürme, ölçeklendirme ve eğme işlemleri yapmanızı sağlar.*</li></ul>
» [3D Dönüşümler.](#-3d-transforms) | <ul><li>**@mixin transform3d()**</li><li>*Elementleri 3D dönüşümler kullanarak biçimlendirmenizi sağlar.*</li></ul>
» [Input Placeholder Özelliklerini Değiştirme.](#-change-input-placeholder-attributes) | <ul><li>**@mixin change-input-placeholder()**</li><li>*Input placeholder özelliklerini değiştirmek için kullanılır.*</li></ul>
» [Yatay Navigasyon Barı.](#-horizontal-navigation-bar) | <ul><li>**@mixin horizontal-navbar()**</li><li>*Yatay menü eklemek için kullanılır.*</li></ul>
» [Dikey Navigasyon Barı.](#-vertical-navigation-bar) | <ul><li>**@mixin vertical-navbar()**</li><li>*Dikey menü eklemek için kullanılır.*</li></ul>
» [Dropdown.](#-dropdown) | <ul><li>**@mixin dropdown()**</li><li>*Açılır menü ekler.*</li></ul>
» [Tooltip.](#-tooltip) | <ul><li>**@mixin tooltip()**</li><li>*İpucu balonu ekler.*</li></ul>
» [Kutu Gölgesi.](#-box-shadow) | <ul><li>**@mixin boshadow()**</li><li>*Kutu gölgesi ekler.*</li></ul>
» [Gradientler.](#-gradients) | <ul><li>**@mixin gradient()**</li><li>*Gradient ekler.*</li></ul>
» [Resim Filtreleri.](#-image-filters) | <ul><li>**@mixin image-filter()**</li><li>*Resimlere efekt veya filtre eklemek için kullanılır.*</li></ul>
» [Buton Animasyonu.](#-button-animation) | <ul><li>**@mixin button-animation()**</li><li>*Animasyonlu butonlar oluşturur.*</li></ul>
» [Font İkon.](#-font-icon) | <ul><li>**@mixin icon()**</li><li>*İstediğiniz renk ve boyutta ikon ekler. 693 ikon mevcuttur.*</li></ul>
» [Font Seçici.](#-font-selector) | <ul><li>**@mixin font()**</li><li>*Elementlere pratik şekilde font eklemek için kullanılır.*</li></ul>
» [Menü Butonu.](#-menu-button) | <ul><li>**@mixin menu-button()**</li><li>*Mobil görünümler için menü butonu ekler.*</li></ul>
» [Üçgen.](#-triangle) | <ul><li>**@mixin triangle()**</li><li>*Herhangi bir elemente üçgen eklemek için.*</li></ul>
» [Metin Gölgesi.](#-text-shadow) | <ul><li>**@mixin text-shadow()**</li><li>*Metin elementine gölge eklemek için.*</li></ul>
» [Bilgi Çubuğu.](#-info-bar) | <ul><li>**@mixin infobar()**</li><li>*Ekrana bilgi çubuğu ekler.*</li></ul>

* **Yardımcılar »**

Açıklama | Özellik
------------ | -------------
» [Clearfix.](#-clearfix) | <ul><li>**%clearfix**</li><li>*Float kullanılan alanları temizlemek için hızlı yol.*</li></ul>
» [Affix.](#-affix) | <ul><li>**%affitop, %affibottom**</li><li>*Üst veya alt kısma sabit alan eklemek için.*</li></ul>


## Lisans

MIT License

## Diğer Lisanslar

* [Font Awesome](https://fortawesome.github.io/Font-Awesome/license/)
* [Bootstrap](https://github.com/twbs/bootstrap/blob/master/LICENSE)
* [Normalize.css](https://github.com/necolas/normalize.css/blob/master/LICENSE.md)

## Katkıda Bulunma

Pull request'ler memnuniyetle karşılanır. Büyük değişiklikler için lütfen önce bir issue açın.


## Yazar

Levent Özbilgiç


---

**Not:** Tüm mixin'lerin ve fonksiyonların detaylı kullanımı için lütfen [tam dokümantasyona](README.md#features) bakın.
