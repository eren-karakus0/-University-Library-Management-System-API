# OpenAPI Tasarımı Ödevi Teslim Raporu

## 👤 Öğrenci Bilgileri
- **Ad Soyad**: Muhammet Eren Karakuş
- **Öğrenci Numarası**: 170422020

---

## 📂 OpenAPI YAML Dosyası

- **openapi.yaml** dosyası projenin GitHub reposuna yüklenmiştir.
- Swagger Editor ile test edilmiş ve doğrulanmıştır.

### 🔗 GitHub Repo Linki
https://github.com/eren-karakus0/UniversityLibraryManagementSystemAPI

---

## 📝 API Açıklaması

### Varlıklar (Entities)
Tasarlanan API'de üç ana varlık yer almaktadır:

1. **books**: Kütüphane kitaplarının yönetimi
   - UUID formatında benzersiz kimlik
   - Başlık, yazar, ISBN-13, yayınevi bilgileri
   - Sayfa sayısı ve stok takibi

2. **students**: Öğrenci kayıtlarının yönetimi
   - UUID formatında benzersiz kimlik
   - Ad-soyad, öğrenci numarası, e-posta
   - Aktiflik durumu takibi

3. **loans**: Kitap ödünç alma işlemlerinin yönetimi
   - Öğrenci ve kitap ilişkilendirmesi
   - Ödünç alma ve iade tarihleri
   - Durum takibi (devam eden, iade edilen, geciken)

### CRUD İşlemleri
Her varlık için standart REST endpoint'leri sağlanmıştır:

- **books**: `GET /books`, `GET /books/{id}`, `POST /books`, `PUT /books/{id}`, `DELETE /books/{id}`
- **students**: `GET /students`, `GET /students/{id}`, `POST /students`, `PUT /students/{id}`, `DELETE /students/{id}`
- **loans**: `GET /loans`, `GET /loans/{id}`, `POST /loans`, `PATCH /loans/{id}/return`

### Components Kullanımı

**Schemas**: Tüm varlıklar için ayrı şemalar tanımlanmıştır:
- Ana varlık şemaları (Book, Student, Loan)
- Create/Update şemaları (validation kuralları ile)
- Yardımcı şemalar (Pagination, Error, LoanStatus enum)

**Parameters**: Yeniden kullanılabilir parametre tanımları:
- Path parametreleri (BookIdParam, StudentIdParam, LoanIdParam)
- Query parametreleri (PageParam, SizeParam)
- Filtreleme parametreleri

**Responses**: Standart HTTP yanıt şablonları:
- 200, 201 (başarılı işlemler)
- 400 (geçersiz istek)
- 404 (kaynak bulunamadı)
- 500 (sunucu hatası)

### Sayfalama ve Hata Durumları

**Sayfalama**: `GET /books` endpoint'inde uygulanmıştır:
- `page` ve `size` query parametreleri
- Yanıtta pagination metadata (total, totalPages)
- Varsayılan değerler ve sınırlamalar

**Hata Durumları**: Tutarlı hata formatı kullanılmıştır:
- Standart hata şeması (Error schema)
- HTTP status kodlarına uygun yanıtlar
- Detaylı hata açıklamaları ve örnekler

---

## 🧪 Test Notları

Swagger Editor üzerinden yapılan testler:

### `GET /books` Testi
- Sayfalama parametreleri ile birlikte çalışır
- Filtreleme parametreleri (title, author) desteklenir
- Yanıt: kitap listesi + pagination metadata

**Örnek Yanıt**:
```json
{
  "data": [
    {
      "id": "550e8400-e29b-41d4-a716-446655440000",
      "title": "Clean Code",
      "author": "Robert C. Martin",
      "isbn": "978-0132350884",
      "publisher": "Prentice Hall",
      "pageCount": 464,
      "stock": 5
    }
  ],
  "pagination": {
    "page": 1,
    "size": 10,
    "total": 25,
    "totalPages": 3
  }
}
```

### `POST /students` Testi 
**Örnek RequestBody**:
```json
{
  "name": "Ahmet Yılmaz",
  "studentNumber": "20210001",
  "email": "ahmet.yilmaz@university.edu.tr",
  "isActive": true
}
```

### Hata Durumu Testi
**400 Bad Request Örneği**:
```json
{
  "error": "VALIDATION_ERROR",
  "message": "Gönderilen veriler geçerli değil",
  "details": {
    "field": "isbn",
    "reason": "ISBN formatı geçersiz"
  }
}
```

---

## 📌 Ek Açıklamalar

### Güvenlik
- JWT Bearer token ve API Key authentication seçenekleri tanımlanmıştır
- Tüm endpoint'ler güvenlik gereksinimi ile korunmuştur

### Validation
- ISBN için regex pattern kullanılmıştır
- E-posta format validasyonu uygulanmıştır
- String uzunluk limitleri ve sayısal minimum/maksimum değerler belirlenmiştir

### Tasarım Prensipleri
- RESTful API standartlarına uygun endpoint isimlendirmesi
- Tutarlı yanıt formatları
- Açıklayıcı documentation ve örnekler
- Yeniden kullanılabilir component'ler

### OpenAPI 3.1.0 Özellikler
- Modern OpenAPI spesifikasyonu kullanılmıştır
- JSON Schema draft 2020-12 desteği
- Nullable fields için doğru syntax

API tasarım