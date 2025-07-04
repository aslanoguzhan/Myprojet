# Ürün Listesi - Vue.js Projesi

Bu proje, Vue.js kullanarak geliştirilmiş örnek bir ürün yönetim uygulamasıdır. Kullanıcılar ürünleri görüntüleyebilir, ekleyebilir, düzenleyebilir ve silebilir.

## 🚀 Özellikler

- ✅ **Ürün Listeleme**: Tüm ürünleri kart formatında görüntüleme
- ✅ **Ürün Ekleme**: Yeni ürün ekleme formu ile ürün bilgilerini kaydetme
- ✅ **Ürün Düzenleme**: Mevcut ürünleri güncelleyebilme
- ✅ **Ürün Silme**: İstenmeyen ürünleri silme (onay ile)
- ✅ **Responsive Tasarım**: Mobil ve masaüstü uyumlu arayüz
- ✅ **Modern UI**: Temiz ve kullanıcı dostu tasarım

## 🛠️ Kullanılan Teknolojiler

- **Vue.js 3**: Ana framework
- **Vue CLI**: Proje yönetimi
- **HTML5**: Yapısal içerik
- **CSS3**: Styling ve responsive tasarım
- **JavaScript ES6+**: Uygulama mantığı

## 📋 Ürün Özellikleri

Her ürün şu bilgileri içerir:
- **Ürün Adı**: Ürünün ismi
- **Fiyat**: Ürünün fiyatı (₺ formatında)
- **Kategori**: Ürün kategorisi (Elektronik, Giyim, Kitap, Ev & Yaşam, Spor)
- **Açıklama**: Ürün hakkında detaylı bilgi (opsiyonel)

## 🎯 Kullanım

### Ürün Ekleme
1. "➕ Yeni Ürün Ekle" butonuna tıklayın
2. Formu doldurun (tüm alanlar zorunlu, açıklama hariç)
3. "Ekle" butonuna tıklayın

### Ürün Düzenleme
1. Düzenlemek istediğiniz ürünün "✏️ Düzenle" butonuna tıklayın
2. Açılan formda gerekli değişiklikleri yapın
3. "Güncelle" butonuna tıklayın

### Ürün Silme
1. Silmek istediğiniz ürünün "🗑️ Sil" butonuna tıklayın
2. Çıkan onay mesajında "Tamam"a tıklayın

## 🏃‍♂️ Projeyi Çalıştırma

### Gereksinimler
- Node.js (v14 veya üzeri)
- Yarn veya npm

### Kurulum
```bash
# Proje klasörüne gidin
cd urun-listesi

# Bağımlılıkları yükleyin
yarn install
# veya
npm install

# Geliştirme sunucusunu başlatın
yarn serve
# veya
npm run serve
```

### Erişim
Uygulama başarıyla başlatıldıktan sonra tarayıcınızda şu adresi açın:
```
http://localhost:8080
```

## 📁 Proje Yapısı

```
urun-listesi/
├── public/
│   ├── index.html          # Ana HTML dosyası
│   └── favicon.ico         # Site ikonu
├── src/
│   ├── components/
│   │   └── ProductList.vue # Ürün listesi ana bileşeni
│   ├── assets/             # Statik dosyalar
│   ├── App.vue            # Ana uygulama bileşeni
│   └── main.js            # Uygulama giriş noktası
├── package.json           # Proje bağımlılıkları
└── README.md             # Bu dosya
```

## 🎨 Tasarım Özellikleri

- **Responsive Grid**: Ürünler otomatik olarak ekran boyutuna göre düzenlenir
- **Hover Efektleri**: Kartlar ve butonlar üzerinde geçiş efektleri
- **Color Coding**: Her buton türü için farklı renk kodlaması
- **Modern Typography**: Okunabilir ve estetik font kullanımı
- **Box Shadows**: Derinlik hissi veren gölge efektleri

## 📱 Responsive Tasarım

Uygulama farklı ekran boyutlarında optimize edilmiştir:
- **Desktop**: Çoklu sütun grid layout
- **Tablet**: Orta boyut ekranlar için optimize edilmiş
- **Mobile**: Tek sütun layout, büyük dokunma alanları

## 🔧 Geliştirme Notları

### Veri Yönetimi
- Ürün verileri bileşen içinde `data()` fonksiyonunda tutulur
- Değişiklikler anlık olarak reaktif şekilde güncellenir
- ID'ler otomatik olarak artan şekilde atanır

### Form Validasyonu
- HTML5 validasyonu kullanılır
- Zorunlu alanlar `required` attribute'u ile belirtilir
- Sayısal alanlar için tip kontrolü yapılır

### Kullanıcı Deneyimi
- İşlem onayları için `confirm()` dialog'u kullanılır
- Form gönderimi için `prevent` modifier'ı ile sayfa yenilenmesi engellenir
- Hover ve focus durumları için görsel geri bildirimler

## 🚀 Üretim Build'i

Üretim için optimize edilmiş build oluşturmak için:

```bash
yarn build
# veya
npm run build
```

Bu komut `dist/` klasöründe deploy edilmeye hazır dosyalar oluşturur.

## 📝 Lisans

Bu proje eğitim amaçlı geliştirilmiştir ve örnek kullanım içindir.

## 👨‍💻 Geliştirici Notları

- Vue.js 3 Composition API yerine Options API kullanılmıştır
- Scoped CSS ile stil kirliliği önlenmiştir
- ES6+ özellikler kullanılmıştır (arrow functions, spread operator, etc.)
- Modern JavaScript best practices uygulanmıştır
