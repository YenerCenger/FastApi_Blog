# FastAPI Blog

Modern bir blog uygulaması. FastAPI, SQLAlchemy ve Jinja2 template engine kullanılarak geliştirilmiştir.

## Özellikler

- Kullanıcı yönetimi (CRUD işlemleri)
- Blog post yönetimi (CRUD işlemleri)
- Post arama fonksiyonu
- Sayfalama (pagination) desteği
- Post görüntülenme sayacı (view counter)
- Kullanıcı profil resimleri
- Responsive web arayüzü
- RESTful API endpoints
- Otomatik API dokümantasyonu (Swagger UI)

## Teknolojiler

- **FastAPI**: Modern, hızlı web framework
- **SQLAlchemy**: ORM (Object-Relational Mapping)
- **SQLite**: Veritabanı
- **Jinja2**: Template engine
- **Bootstrap 5**: CSS framework
- **Pydantic**: Veri validasyonu

## Kurulum

### Gereksinimler

- Python 3.12 veya üzeri
- uv (paket yöneticisi)

### Adımlar

1. Projeyi klonlayın veya indirin:
```bash
git clone <repository-url>
cd Fastapi_blog
```

2. Sanal ortamı oluşturun ve aktifleştirin:
```bash
uv venv
# Windows
.venv\Scripts\activate
# Linux/Mac
source .venv/bin/activate
```

3. Bağımlılıkları yükleyin:
```bash
uv sync
```

4. Uygulamayı çalıştırın:
```bash
uv run fastapi dev main.py
```

Uygulama `http://127.0.0.1:8000` adresinde çalışacaktır.

## Proje Yapısı

```
Fastapi_blog/
├── main.py              # Ana uygulama dosyası
├── database.py          # Veritabanı bağlantı ayarları
├── models.py            # SQLAlchemy modelleri
├── schemas.py           # Pydantic şemaları
├── routers/             # API route'ları
│   ├── __init__.py
│   ├── users.py        # Kullanıcı endpoint'leri
│   └── posts.py        # Post endpoint'leri
├── templates/           # Jinja2 template'leri
│   ├── layout.html
│   ├── home.html
│   ├── post.html
│   ├── user_posts.html
│   └── error.html
├── static/              # Statik dosyalar (CSS, JS, resimler)
│   ├── css/
│   ├── js/
│   └── icons/
├── media/               # Yüklenen dosyalar
│   └── profile_pics/
└── blog.db             # SQLite veritabanı
```

## API Endpoints

### Kullanıcı Endpoints

- `GET /api/users` - Tüm kullanıcıları listele
- `GET /api/users/{user_id}` - Belirli bir kullanıcıyı getir
- `POST /api/users` - Yeni kullanıcı oluştur
- `PATCH /api/users/{user_id}` - Kullanıcı bilgilerini güncelle
- `DELETE /api/users/{user_id}` - Kullanıcıyı sil

### Post Endpoints

- `GET /api/posts` - Tüm postları listele
- `GET /api/posts/{post_id}` - Belirli bir postu getir
- `POST /api/posts` - Yeni post oluştur
- `PUT /api/posts/{post_id}` - Postu tamamen güncelle
- `PATCH /api/posts/{post_id}` - Postu kısmen güncelle
- `DELETE /api/posts/{post_id}` - Postu sil

### Web Sayfaları

- `GET /` veya `GET /posts` - Ana sayfa (post listesi, sayfalama ile)
- `GET /posts/{post_id}` - Post detay sayfası
- `GET /users/{user_id}/posts` - Kullanıcının postları
- `GET /search?text=...` - Post arama sayfası

## Kullanım

### API Dokümantasyonu

Uygulama çalıştıktan sonra aşağıdaki adreslerden API dokümantasyonuna erişebilirsiniz:

- Swagger UI: `http://127.0.0.1:8000/docs`
- ReDoc: `http://127.0.0.1:8000/redoc`

### Örnek API İstekleri

#### Kullanıcı Oluşturma

```bash
curl -X POST "http://127.0.0.1:8000/api/users" \
  -H "Content-Type: application/json" \
  -d '{
    "username": "testuser",
    "email": "test@example.com"
  }'
```

#### Post Oluşturma

```bash
curl -X POST "http://127.0.0.1:8000/api/posts" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "İlk Post",
    "content": "Bu benim ilk postum.",
    "user_id": 1
  }'
```

#### Post Arama

```bash
curl "http://127.0.0.1:8000/api/posts/search?text=python"
```

## Veritabanı

Uygulama SQLite veritabanı kullanır. İlk çalıştırmada `blog.db` dosyası otomatik olarak oluşturulur.

### Modeller

**User Model:**
- id: Birincil anahtar
- username: Benzersiz kullanıcı adı (max 50 karakter)
- email: Benzersiz e-posta adresi (max 120 karakter)
- image_file: Profil resmi dosya adı (opsiyonel)

**Post Model:**
- id: Birincil anahtar
- title: Post başlığı (max 100 karakter)
- content: Post içeriği
- user_id: Kullanıcı foreign key
- date_posted: Oluşturulma tarihi
- view: Görüntülenme sayısı

## Özellikler Detayı

### Sayfalama

Ana sayfada postlar sayfa başına 5 adet gösterilir. URL'de `?page=2` parametresi ile farklı sayfalara geçilebilir.

### Arama

Post arama fonksiyonu başlık ve içerikte arama yapar. Büyük/küçük harf duyarsızdır.

### Görüntülenme Sayacı

Her post detay sayfası ziyaret edildiğinde görüntülenme sayısı otomatik olarak artar.

### Profil Resimleri

Kullanıcılar profil resmi yükleyebilir. Yüklenen resimler `media/profile_pics/` klasöründe saklanır. Resim yüklenmemişse varsayılan resim gösterilir.

## Geliştirme

### Kod Yapısı

- **Routers**: API endpoint'leri router modüllerinde organize edilmiştir
- **Models**: Veritabanı modelleri SQLAlchemy ile tanımlanmıştır
- **Schemas**: Pydantic şemaları veri validasyonu için kullanılır
- **Templates**: Jinja2 template'leri web arayüzü için kullanılır

### Bağımlılıklar

Bağımlılıklar `pyproject.toml` dosyasında tanımlanmıştır ve `uv` ile yönetilir.

## Lisans

Bu proje eğitim amaçlı geliştirilmiştir.

## Notlar

- Kullanıcı kimlik doğrulama henüz implement edilmemiştir
- `user_id` alanı geçici olarak manuel olarak sağlanmaktadır
- Üretim ortamı için güvenlik önlemleri eklenmelidir
