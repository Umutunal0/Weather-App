# Weather App (Hava Durumu Uygulaması)

## Proje Hakkında

Bu proje, bir şehir arama ve hava durumu bilgisi alma uygulamasıdır. Proje, Vue.js ve Tailwind CSS kullanılarak geliştirilmiştir ve OpenWeather API ile entegre edilmiştir. Amaç, kullanıcıların bir şehir aratarak hava durumu bilgilerine ulaşmasını sağlamaktır.

### **Özellikler**
- Şehir arama ve öneri listesi
- Seçilen şehir bilgilerini görüntüleme (Hava durumu API'si üzerinden)
- Tailwind CSS ile responsive tasarım
- Vue Router kullanımı ile yönlendirme

### **Tamamlanan Kısımlar**
- Şehir arama alanı ve sonuçların görüntülenmesi
- Kullanıcı seçimlerinin Vue Router ile yönlendirilmesi
- Geocoding API kullanılarak şehir enlem ve boylam bilgisi alınması

### **Eksik Kalan Kısımlar**
- Seçilen şehrin hava durumu verilerinin One Call API üzerinden görüntülenmesi
- API'den dönen hataların daha iyi yönetimi (401 Unauthorized hatası çözülmedi)
- Daha fazla test ve hata ayıklama

### **Karşılaşılan Zorluklar**
- Vue.js ve Tailwind CSS ile ilk kez çalıştığım için bu teknolojilere alışma sürecim oldu.
- OpenWeather API bağlantılarında yetkilendirme ve veri çekme konusunda bazı teknik problemler yaşadım.
- API yanıtlarını işlemede hatalar oluştu ve bu hatalar çözüm için daha fazla zamana ihtiyaç duyuyor.

---

## **Kullanılan Teknolojiler**
- **Vue.js (v3)**: Frontend geliştirme
- **Tailwind CSS**: CSS framework
- **Axios**: API çağrıları
- **OpenWeather API**: Hava durumu verisi almak için kullanıldı

---

## **Kurulum ve Çalıştırma**

Projeyi çalıştırmak için aşağıdaki adımları izleyin:

1. **Depoyu klonlayın:**
   ```bash
   git clone https://github.com/kullaniciadi/weather-app.git
   cd weather-app

2. **Project Setup

npm install

3. Compile and Hot-Reload for Development


npm run dev

4. Projeyi tarayıcıda açın:

http://localhost:5173 adresine gidin.

API Kullanımı
Projede kullanılan OpenWeather API:

Geocoding API: Şehir enlem ve boylam bilgilerini almak için.
One Call API 3.0: Hava durumu verilerini almak için.
Lütfen API anahtarınızı .env dosyasına ekleyin:

VITE_OPENWEATHER_API_KEY=YOUR_API_KEY


** Geliştirme Süreci
Bu projede:

Vue.js ve Tailwind CSS ile ilk kez çalıştım.
OpenWeather API entegrasyonu yapmayı öğrendim.
Yeni bir teknolojiyle proje geliştirme sürecinde nasıl ilerlemem gerektiği konusunda deneyim kazandım.


** Gelecekte Yapılacaklar
API hatalarının çözülmesi ve hava durumu verilerinin düzgün görüntülenmesi.
Projede testlerin eklenmesi.
Daha iyi responsive tasarım ve kullanıcı deneyimi geliştirme.


