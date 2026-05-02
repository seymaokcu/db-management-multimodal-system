# db-management-multimodal-system
Otomatik bir veri hattı, Google Gemini AI ve n8n kullanarak çok modlu girdileri (metin ve görüntü) işler ve yapılandırılmış analizleri Supabase'de depolar.

Multimodal AI Data Pipeline (Gemini & Supabase)

Bu proje, metin ve görseller gibi yapılandırılmamış verileri alıp anlamlı, düzenli veritabanı kayıtlarına dönüştüren uçtan uca bir Yapay Zeka Veri Hattı mimarisi sunuyor. En güncel büyük dil modelleriyle (LLM) modern düşük kodlu otomasyon araçlarını bir arada kullanıyor.

🚀 Proje Hakkında

Sistem şöyle çalışıyor: Bir müşteri geri bildirimi (yani metin) ile bir ürün fotoğrafını (görseli) aynı anda alıyor. Yapay zeka, bu iki farklı veriyi bir araya getiriyor, duygusal analiz yapıyor ve kategorilendiriyor. Ardından, temizlenen bu veriler kalıcı olarak bir PostgreSQL tablosunda saklanıyor.

🛠️ Teknoloji Yığını

n8n: İş akışı otomasyonu ve veri akışını yönetiyor.
Google Gemini 2.5 Flash: Hem metni hem görseli analiz ediyor.
Supabase (PostgreSQL): Bulut tabanlı ilişkisel veritabanını sağlıyor.
JavaScript: Yapay zekadan gelen çıktıyı temizliyor, JSON formatına çeviriyor.
Postman: Sistemi HTTP POST istekleriyle test etmek için kullanıldı.

🏗️ Sistem Mimarisi (Workflow)

Sistem toplam beş ana aşamadan oluşuyor:

1. Webhook Node: Dışarıdan gelen JSON veriyi karşılar.
2. HTTP Request Node: Verilen görsel linkinden dosyayı indirir.
3. Gemini AI Node: Metin ve görseli analiz eder, duyguyu (pozitif/negatif) ve kategoriyi belirler.
4. JavaScript Node: AI’dan gelen veriyi temizler, net bir JSON objesine dönüştürür.
5. Supabase Node: Son olarak, ayrıştırılmış verileri multimodal_analysis tablosuna kaydeder.


Veritabanı Şeması
Bu proje kapsamında Supabase üzerinde oluşturulan multimodal_analysis tablosunun yapısı aşağıdadır:

:---:Sütun	Tip	Açıklama
id	              int8 (PK)	    Benzersiz kimlik numarası (Auto-increment)
original_text	    text	        Kullanıcının gönderdiği ham metin
image_url	        text	        Analiz edilen görselin linki
category	        text	        AI tarafından belirlenen kategori
sentiment	        text	        AI tarafından belirlenen duygu durumu
created_at	      timestamp	    İşlemin gerçekleştiği zaman



⚙️ Kurulum ve Kullanım
1.Bu depodaki workflow.json dosyasını indirin ve n8n arayüzüne içe aktarın (Import).

2.Kendi Gemini API anahtarınızı ve Supabase bağlantı bilgilerinizi (URL ve Service Role Key) tanımlayın.

3.n8n'de Active modunu açın.

4.Postman üzerinden Production URL adresine aşağıdaki formatta veri gönderin:

JSON
{
  "text": "Siparişim rekor hızda elime ulaştı, paketleme harikaydı!",
  "image_url": "https://example.com/urun-fotografi.jpg"
}

n8n EKRANI
<img width="1865" height="948" alt="image" src="https://github.com/user-attachments/assets/64fa3847-e3af-42f8-81a9-f7aca851a3aa" />

SUPABASE DATABASE TABLOSU
<img width="1856" height="944" alt="image" src="https://github.com/user-attachments/assets/28425535-b680-4ed1-b3f8-d7a26a2f0f3f" />

SUPABASE DATABASE
<img width="1860" height="945" alt="image" src="https://github.com/user-attachments/assets/72210f08-1973-4f0e-8a6d-3e9faf3c1893" />

POSTMAN 
<img width="1594" height="1024" alt="image" src="https://github.com/user-attachments/assets/29a01991-7c79-4b2e-a030-f9f03a478c7f" />
<img width="1595" height="1024" alt="image" src="https://github.com/user-attachments/assets/103d283f-3536-4be6-a254-1dcaecad008a" />
























Kısacası, bu sistem sayesinde ham metin ve görsellerden düzenli, kullanıma hazır verilere kolayca ulaşmak mümkün oluyor.
