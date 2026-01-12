MAUN SOSYAL ADMIN PANEL - README

================================================================================
PROJE TANIMI
================================================================================

MAUN Sosyal Admin Panel, MAUN Sosyal platformunun yönetim arayuzudur. Bu proje,
universite ogrencilerinin sosyal medya deneyimini guvenli ve etkili bir sekilde
yonetmek amaciyla gelistirilmistir. Admin paneli sayesinde platform yoneticileri
kullanici hesaplarini, gonderileri ve sistem istatistiklerini merkezi bir
arayuzden kontrol edebilir.

Proje kapsaminda asagidaki temel ozellikler uygulanmistir:
- Kullanici yonetimi (kayit, yasaklama, profil guncelleme)
- Gonderi moderasyonu (goruntuleme, silme)
- Sistem analizi (istatistikler, aktivite takibi)
- Guvenli giris sistemi (OTP tabanli kimlik dogrulama)

================================================================================
KULLANILAN TEKNOLOJILER
================================================================================

Frontend Teknolojileri:
- React 18.3.1 - Kullanici arayuzu kutuphanesi
- TypeScript 5.5.3 - Tip guvenligi saglayan JavaScript ustkumesi
- Vite 5.4.8 - Hizli gelistirme sunucusu ve build araci
- Tailwind CSS 3.4.1 - Utility-first CSS framework
- Lucide React - SVG ikon kutuphanesi

Backend Teknolojileri:
- Laravel + Sanctum - PHP framework ve API kimlik dogrulama
- MySQL - Veritabani yonetim sistemi
- RESTful API - HTTP tabanli servis mimarisi

Gelistirme Araclari:
- Node.js 18+ - JavaScript runtime
- npm - Paket yoneticisi
- VS Code - Kod editoru

================================================================================
SISTEM MIMARISI
================================================================================

Proje, modern web uygulamalari icin standart olan client-server mimarisini
kullanmaktadir:

Frontend (Client Side):
- React tabanli tek-sayfali uygulama (SPA)
- Component-based architecture
- State management (useState, useEffect)
- Responsive tasarim (mobil uyumlu)

Backend (Server Side):
- Laravel REST API
- JWT token tabanli kimlik dogrulama
- CRUD islemleri icin endpoint'ler
- Admin yetkileri ile korunan rotalar

Veri Akisi:
Kullanici -> React UI -> API Client -> REST API -> Database -> Response -> UI

================================================================================
KIMLIK DOGRULAMA SISTEMI (OTP + TOKEN)
================================================================================

Sistem, iki adimli guvenli giris sureci kullanmaktadir:

1. OTP (One-Time Password) Asamasi:
   - Kullanici email adresini girer
   - Sistem backend'e /login istegi gonderir
   - Backend email'e 6 haneli OTP kodu gonderir
   - Kullanici kodu girerek dogrular

2. Token Yonetimi:
   - Basarili OTP dogrulamasindan sonra JWT token uretilir
   - Token localStorage'da saklanir
   - Her API isteginde Authorization header'ina eklenir
   - Token suresi dolunca otomatik cikis yapilir

Guvenlik Ozellikleri:
- OTP kodlari tek kullanmlik ve zaman sinirli
- Token'lar sifrelenmis ve imza ile korunmus
- Yetkisiz erisimlerde otomatik oturum sonlandirma

================================================================================
ADMIN PANEL OZELLIKLERI
================================================================================

Dashboard (Panel Ozeti):
- Toplam ogrenci, gonderi, begeni ve yorum sayilari
- Son aktiviteler feed'i (gonderi, yorum, begeni)
- Gercek zamanli veri guncelleme

Kullanici Yonetimi:
- Tum kullanicilarin listesi
- Kullanici profili goruntuleme
- Hesap yasaklama/acma islemleri
- Kullanici istatistikleri

Gonderi Yonetimi:
- Tum platform gonderilerinin listesi
- Gonderi detayi goruntuleme
- Sikayet edilen icerik takibi
- Gonderi silme yetkisi

Ayarlar:
- Admin profil bilgilerini guncelleme
- Biyografi, dogum tarihi gibi bilgiler

================================================================================
API – FRONTEND ENTEGRASYONU
================================================================================

Tum backend iletisimi merkezi bir katman uzerinden yonetilir:

API Client (apiClient.ts):
- Singleton pattern ile tek instance
- Tum HTTP istekleri burada toplanmis
- Otomatik token yonetimi
- Error handling ve response parsing
- TypeScript tip guvenligi

Ana Endpoint'ler:
- Authentication: /login, /verify-otp, /logout
- Users: /admin/users, /admin/users/{id}/block
- Posts: /posts, /posts/{id} (DELETE)
- Notifications: /notifications, /notifications/unread-count
- Profile: /profile (PUT)

Veri Akisi:
React Component -> apiClient.method() -> fetch() -> Backend API -> Response -> UI Update

================================================================================
KURULUM VE CALISTIRMA
================================================================================

On Kosullar:
- Node.js 18 veya ustu surumu
- npm paket yoneticisi
- Git versiyon kontrol sistemi

Kurulum Adimlari:

1. Projeyi klonlayin:
   git clone [https://github.com/serhathawk/maun-adminpanel.git]
   cd AdminPanel-MAUN-Sosyal/project

2. Bagimliliklari yukleyin:
   npm install

3. Gelistirme sunucusunu baslatin:
   npm run dev

4. Tarayicida acin:
   http://localhost:5173

Build Islemleri:
- Gelistirme: npm run dev
- Production build: npm run build
- Build kontrolu: npm run build (dist/ klasoru olusur)

================================================================================
GUVENLIK MIMARISI
================================================================================

Cok katmanli guvenlik yaklasimi uygulanmistir:

1. Network Security:
   - HTTPS protokolu (production'da)
   - CORS politikasi
   - Rate limiting

2. Authentication & Authorization:
   - OTP tabanli giris
   - JWT token yetkilendirmesi
   - Admin-only endpoint korumasi
   - Token expiration kontrolu

3. Data Security:
   - Input validation ve sanitization
   - SQL injection korumasi (backend)
   - XSS korumasi
   - Sensitive data encryption

4. Application Security:
   - TypeScript ile tip guvenligi
   - Error boundary'ler
   - Secure coding practices
   - Dependency security audits

================================================================================
GELISTIRME NOTLARI
================================================================================

Kod Organizasyonu:
- src/pages/: Sayfa component'leri
- src/components/: Yeniden kullanilabilir UI elementleri
- src/api/: Backend iletisim katmani
- Component-based architecture
- Separation of concerns prensibi

Gelistirme Standartlari:
- TypeScript strict mode
- ESLint kod kalitesi kontrolu
- Responsive design (mobile-first)
- Accessibility uyumlulugu
- Clean code principles

Test ve Kalite:
- TypeScript compilation kontrolu
- Build success validation
- Manual testing tum ozellikler icin
- Cross-browser compatibility

Performans Optimizasyonlari:
- Lazy loading
- Code splitting (Vite)
- Image optimization
- Bundle size minimization

Versiyon Kontrolu:
- Git ile versiyon yonetimi
- Feature branch workflow
- Commit message standards
- Code review process

================================================================================
GELISTIRENLER
================================================================================

Serhat ŞAHİN - [https://github.com/serhathawk]
Mehdi KARAÇOR - [https://github.com/karacormehdi]




