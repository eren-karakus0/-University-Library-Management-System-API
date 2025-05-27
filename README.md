# 📚 University Library Management System API

Bu proje, üniversite kütüphane sistemi için tasarlanmış RESTful bir API spesifikasyonudur. OpenAPI 3.1.0 standardına uygun olarak geliştirilmiştir.

## 🎯 Proje Amacı

Üniversite kütüphanelerinin dijital dönüşüm sürecinde ihtiyaç duyulan temel işlevleri karşılamak üzere tasarlanmış modern bir API sistemidir. Kitap yönetimi, öğrenci kayıtları ve ödünç alma işlemlerini merkezi bir sistem üzerinden yönetmeyi amaçlar.

## 🏗️ API Mimarisi

### Ana Bileşenler

#### 📖 Books Management
- Kitap CRUD işlemleri
- ISBN tabanlı kayıt sistemi
- Stok takibi
- Gelişmiş arama ve filtreleme

#### 👨‍🎓 Student Management  
- Öğrenci kayıt sistemi
- Aktiflik değişim durumu takibi
- E-posta tabanlı iletişim

#### 🔄 Loan Management
- Kitap ödünç alma sistemi
- Otomatik gecikme tespit
- İade takip sistemi

## 🛠️ Teknik Özellikler

### OpenAPI 3.1.0 Spesifikasyonları
- **Veri Formatları**: JSON
- **Authentication**: JWT Bearer Token + API Key
- **Validation**: Comprehensive schema validation
- **Error Handling**: Standart HTTP status kodları
- **Pagination**: Sayfalama desteği

### Veri Modelleri

#### Book Schema
```yaml
- id: UUID
- title: string
- author: string  
- isbn: string (ISBN-13 format)
- publisher: string
- pageCount: integer
- stock: integer
```

#### Student Schema
```yaml
- id: UUID
- name: string
- studentNumber: string
- email: string (email format)
- isActive: boolean
```

#### Loan Schema
```yaml
- id: UUID
- studentId: UUID
- bookId: UUID
- loanDate: date
- returnDate: date (nullable)
- status: enum [ongoing, returned, late]
```

## 🚀 API Endpoints

### Books
- `GET /books` - Kitap listesi (sayfalama + filtreleme)
- `GET /books/{id}` - Kitap detayı
- `POST /books` - Yeni kitap ekleme
- `PUT /books/{id}` - Kitap güncelleme
- `DELETE /books/{id}` - Kitap silme

### Students
- `GET /students` - Öğrenci listesi
- `GET /students/{id}` - Öğrenci detayı
- `POST /students` - Yeni öğrenci kayıt
- `PUT /students/{id}` - Öğrenci güncelleme
- `DELETE /students/{id}` - Öğrenci silme

### Loans
- `GET /loans` - Ödünç kayıtları
- `GET /loans/{id}` - Ödünç detayı
- `POST /loans` - Kitap ödünç alma
- `PATCH /loans/{id}/return` - Kitap iade

## 💡 Öne Çıkan Özellikler

### Gelişmiş Filtreleme
- Kitap arama (başlık, yazar)
- Öğrenci aktiflik durumu
- Ödünç durumu filtreleme

### Güvenlik
- JWT tabanlı kimlik doğrulama
- API Key desteği
- Rate limiting hazırlığı

### Hata Yönetimi
- Standart HTTP status kodları
- Detaylı hata mesajları
- Validation error details

### Sayfalama
- `page` ve `size` query parametreleri
- Metadata ile toplam sayfa bilgisi
- Performans optimizasyonu

## 📋 Kullanım Örnekleri

### Kitap Arama
```bash
GET /books?title=Clean&author=Martin&page=1&size=10
```

### Öğrenci Kayıt
```json
POST /students
{
  "name": "Ahmet Yılmaz",
  "studentNumber": "20210001", 
  "email": "ahmet@university.edu.tr",
  "isActive": true
}
```

### Kitap Ödünç Alma
```json
POST /loans
{
  "studentId": "550e8400-e29b-41d4-a716-446655440001",
  "bookId": "550e8400-e29b-41d4-a716-446655440000",
  "loanDate": "2024-01-15"
}
```

## 🧪 Test Etme

### Swagger Editor ile Test
1. [Swagger Editor](https://editor.swagger.io) adresini ziyaret edin
2. `openapi.yaml` dosyasının içeriğini kopyalayın
3. Editöre yapıştırın
4. "Try it out" özelliği ile endpoint'leri test edin

### Örnek Test Senaryoları
- Kitap listesi çekme
- Yeni öğrenci kayıt etme
- Ödünç alma işlemi
- Kitap iade etme
- Hata durumları

## 📊 Validation Kuralları

### ISBN Validation
- Format: 978-XXXXXXXXXX
- Regex: `^978-\d{10}$`

### Email Validation
- Standard email format kontrolü
- Unique constraint (implementation level)

### UUID Format
- Tüm ID alanları UUID v4 formatında
- Path parametrelerinde validation

## 🔮 Gelecek Geliştirmeler

### Planlanan Özellikler
- Kitap rezervasyon sistemi
- Gecikme ceza hesaplama
- Bildirim sistemi entegrasyonu
- Raporlama endpoint'leri
- Bulk operations desteği

### Teknik İyileştirmeler
- GraphQL endpoint'leri
- WebSocket real-time updates
- Advanced caching strategies
- Microservice architecture hazırlığı

## 📄 Lisans

Bu proje MIT lisansı altında açık kaynak kodlu olarak geliştirilmiştir.

## 🤝 Katkıda Bulunma

API spesifikasyonuna katkıda bulunmak için:
1. Repository'yi fork edin
2. Feature branch oluşturun
3. Değişikliklerinizi commit edin
4. Pull request gönderin

## 📞 İletişim

- **Proje Sahibi**: [Adınız]
- **E-posta**: [E-posta adresiniz]
- **GitHub**: [GitHub profiliniz]

---

**Not**: Bu API spesifikasyonu eğitim amaçlı olarak hazırlanmıştır ve Açık Kaynak Kodlu Yazılımlar dersi kapsamında geliştirilmiştir.
